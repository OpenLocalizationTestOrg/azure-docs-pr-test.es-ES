---
title: estado de aaaCheck, configurar el registro y reciba alertas - Azure Logic Apps | Documentos de Microsoft
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
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="c343a-103">Supervisar el estado, configurar el registro de diagnósticos y activar alertas para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c343a-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="c343a-104">Después de [crear y ejecutar una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md), puede comprobar su historial de ejecuciones, historial de desencadenadores, estado y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c343a-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="c343a-105">Para la supervisión de eventos en tiempo real y una depuración más rica, configure el [registro de diagnósticos](#azure-diagnostics) de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c343a-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="c343a-106">De este modo, puede [buscar y ver eventos](#find-events), como eventos de desencadenador, eventos de ejecución y eventos de acción.</span><span class="sxs-lookup"><span data-stu-id="c343a-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="c343a-107">También puede usar estos [datos de diagnóstico con otros servicios](#extend-diagnostic-data), como Azure Storage y Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c343a-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="c343a-108">Configurar notificaciones de tooget sobre errores u otros problemas posibles, [alertas](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="c343a-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="c343a-109">Por ejemplo, puede crear una alerta que detecte "cuando se produzcan errores en más de cinco ejecuciones en una hora".</span><span class="sxs-lookup"><span data-stu-id="c343a-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="c343a-110">También puede configurar la supervisión, el seguimiento y el registro mediante programación con la [configuración de eventos y las propiedades de Azure Diagnostics](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="c343a-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="c343a-111">Visualización del historial de ejecuciones y desencadenadores de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c343a-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="c343a-112">toofind la aplicación lógica en hello [portal de Azure](https://portal.azure.com), en Hola menú principal de Azure, elija **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="c343a-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="c343a-113">En el cuadro de búsqueda de hello, busque "logic apps" y elija **aplicaciones lógicas**.</span><span class="sxs-lookup"><span data-stu-id="c343a-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Búsqueda de la aplicación lógica](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="c343a-115">Hola portal de Azure muestra todas las aplicaciones de la lógica de Hola que están asociadas a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c343a-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="c343a-116">Seleccione la aplicación lógica y luego elija **Información general**.</span><span class="sxs-lookup"><span data-stu-id="c343a-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="c343a-117">Hola portal de Azure muestra el historial de ejecuciones de Hola y el historial de desencadenador para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c343a-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="c343a-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c343a-118">For example:</span></span>

   ![Historial de ejecuciones e historial de desencadenadores de la aplicación lógica](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="c343a-120">**Se ejecuta historial** muestra todas las ejecuciones de hello para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c343a-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="c343a-121">**Desencadenar historial** muestra todas las actividades de desencadenador de hello para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c343a-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="c343a-122">Para obtener descripciones de estado, vea [Diagnóstico de errores en las aplicaciones lógicas](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="c343a-123">Si no encuentra datos Hola que espera, en la barra de herramientas de hello, elija **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="c343a-124">Hola tooview los pasos de una ejecución específica, en **ejecuta historial**, seleccione que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="c343a-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="c343a-125">vista de monitor de Hello muestra cada paso en el que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="c343a-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="c343a-126">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c343a-126">For example:</span></span>

   ![Acciones de una ejecución concreta](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="c343a-128">tooget más detalles sobre Hola ejecutar, elija **detalles de la ejecución**.</span><span class="sxs-lookup"><span data-stu-id="c343a-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="c343a-129">Esta información resume los pasos de hello, estado, entradas y salidas de hello ejecutan.</span><span class="sxs-lookup"><span data-stu-id="c343a-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Selección de "Detalles de ejecución"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="c343a-131">Por ejemplo, puede obtener Hola de ejecución **Id. de correlación**, que pueden requerir cuando usas hello [API de REST para las aplicaciones lógicas](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="c343a-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="c343a-132">tooget obtener más información acerca de un paso concreto, elija ese paso.</span><span class="sxs-lookup"><span data-stu-id="c343a-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="c343a-133">Ahora puede revisar detalles como las entradas, las salidas y los errores acontecidos en ese paso.</span><span class="sxs-lookup"><span data-stu-id="c343a-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="c343a-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c343a-134">For example:</span></span>

   ![Detalles del paso](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="c343a-136">Todos los detalles de tiempo de ejecución y eventos se cifran en hello servicio Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="c343a-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="c343a-137">Se descifran solo cuando un usuario solicita tooview esos datos.</span><span class="sxs-lookup"><span data-stu-id="c343a-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="c343a-138">También puede controlar eventos de acceso a toothese con [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="c343a-139">detalles de tooget sobre un evento de desencadenador específico, vuelva atrás toohello **Introducción** panel.</span><span class="sxs-lookup"><span data-stu-id="c343a-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="c343a-140">En **desencadenar historial**, seleccione los eventos de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="c343a-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="c343a-141">Ahora puede revisar detalles como las entradas y salidas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c343a-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Detalles de salida de evento de desencadenador](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="c343a-143">Activación del registro de diagnósticos de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c343a-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="c343a-144">Para una depuración más rica con detalles y eventos de runtime, puede configurar el registro de diagnósticos con [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="c343a-145">Análisis de registros es un servicio en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) que supervisa la nube y locales toohelp entornos mantener su disponibilidad y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c343a-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="c343a-146">Antes de empezar, deberá toohave un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="c343a-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="c343a-147">Obtenga información acerca de [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="c343a-148">Hola [portal de Azure](https://portal.azure.com), busque y seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c343a-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="c343a-149">En el menú de hoja de la aplicación de lógica hello, en **supervisión**, elija **diagnósticos** > **configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="c343a-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Vaya a configuración de diagnóstico de tooMonitoring, diagnósticos,](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="c343a-151">En **Configuración de diagnóstico**, elija **Activado**.</span><span class="sxs-lookup"><span data-stu-id="c343a-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activación de los registros de diagnóstico](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="c343a-153">Ahora seleccione categoría de evento y el área de trabajo OMS de hello para el registro como se muestra:</span><span class="sxs-lookup"><span data-stu-id="c343a-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="c343a-154">Seleccione **enviar tooLog análisis**.</span><span class="sxs-lookup"><span data-stu-id="c343a-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="c343a-155">En **Log Analytics**, elija **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="c343a-156">En **áreas de trabajo de OMS**, seleccione toouse de área de trabajo OMS de hello para el registro.</span><span class="sxs-lookup"><span data-stu-id="c343a-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="c343a-157">En **registro**, seleccione hello **WorkflowRuntime** categoría.</span><span class="sxs-lookup"><span data-stu-id="c343a-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="c343a-158">Elija el intervalo de métrica de saludo.</span><span class="sxs-lookup"><span data-stu-id="c343a-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="c343a-159">Cuando termine, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-159">When you're done, choose **Save**.</span></span>

   ![Selección del área de trabajo de OMS y los datos para el registro](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="c343a-161">Ahora puede buscar eventos y otros datos de los eventos de desencadenador, los eventos de ejecución y los eventos de acción.</span><span class="sxs-lookup"><span data-stu-id="c343a-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="c343a-162">Búsqueda de eventos y datos de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c343a-162">Find events and data for your logic app</span></span>

<span data-ttu-id="c343a-163">toofind y ver los eventos en la aplicación lógica, como eventos de desencadenador, ejecute los eventos y los eventos de acción, siguen estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c343a-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="c343a-164">Hola [portal de Azure](https://portal.azure.com), elija **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="c343a-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c343a-165">Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="c343a-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Selección de "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="c343a-167">En **Log Analytics**, busque y seleccione el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="c343a-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selección del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="c343a-169">En **Administración**, elija **Portal de OMS**.</span><span class="sxs-lookup"><span data-stu-id="c343a-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Selección de "Portal de OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="c343a-171">En la página principal de OMS, seleccione **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="c343a-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="c343a-173">O bien</span><span class="sxs-lookup"><span data-stu-id="c343a-173">-or-</span></span>

   ![En el menú OMS de hello, elija "Búsqueda de registros"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="c343a-175">En el cuadro de búsqueda de hello, especificar un campo que desea que toofind y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="c343a-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="c343a-176">Cuando empiece a escribir, OMS le mostrará posibles coincidencias y operaciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="c343a-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="c343a-177">Por ejemplo, toofind Hola primeros 10 eventos que se produjeron, escriba y seleccione esta consulta de búsqueda: **categoría = WorkflowRuntime | top 10**</span><span class="sxs-lookup"><span data-stu-id="c343a-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Especificación de cadena de búsqueda](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="c343a-179">Obtenga más información sobre [cómo toofind datos de análisis de registros](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="c343a-180">En la página de resultados de hello, en la barra de la izquierda hello, elija Hola período de tiempo que desea tooview.</span><span class="sxs-lookup"><span data-stu-id="c343a-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="c343a-181">Elija la consulta agregando un filtro de toorefine **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Selección del marco temporal de los resultados de la consulta](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="c343a-183">En **agregar filtros**, escriba el nombre de filtro de Hola para que pueda encontrar el filtro de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="c343a-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="c343a-184">Seleccione el filtro de Hola y elija **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="c343a-185">Este ejemplo usa hello word "status" toofind no pudo eventos bajo **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="c343a-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="c343a-186">Hola aquí el filtro para **status_s** ya está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c343a-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Selección de filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="c343a-188">En la barra de la izquierda hello, seleccione el valor de filtro de Hola que desee toouse y elija **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Selección del valor de filtro y de "Aplicar"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="c343a-190">Consulta de toohello devuelven ahora que va a compilar.</span><span class="sxs-lookup"><span data-stu-id="c343a-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="c343a-191">La consulta se ha actualizado con el filtro y el valor seleccionados.</span><span class="sxs-lookup"><span data-stu-id="c343a-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="c343a-192">Los resultados anteriores también se filtraron.</span><span class="sxs-lookup"><span data-stu-id="c343a-192">Your previous results are now filtered too.</span></span>

   ![Devolver tooyour consulta con los resultados filtrados](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="c343a-194">Elija de la consulta para un uso futuro, toosave **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c343a-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="c343a-195">Obtenga información acerca de [cómo toosave la consulta](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="c343a-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="c343a-196">Extensión de cómo y dónde usa los datos de diagnóstico con otros servicios</span><span class="sxs-lookup"><span data-stu-id="c343a-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="c343a-197">Además de con Azure Log Analytics, puede usar los datos de diagnóstico de la aplicación lógica con otros servicios de Azure, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c343a-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="c343a-198">Archivar registros de Diagnósticos de Azure en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c343a-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="c343a-199">Transmitir tooAzure centros de eventos de los registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="c343a-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="c343a-200">Luego puede obtener supervisión en tiempo real mediante la telemetría y los análisis de otros servicios, como [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) y [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="c343a-201">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c343a-201">For example:</span></span>

* [<span data-ttu-id="c343a-202">Datos de la secuencia de los centros de eventos tooStream análisis</span><span class="sxs-lookup"><span data-stu-id="c343a-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="c343a-203">Analizar datos que se están transmitiendo con Stream Analytics y crear un panel de análisis en tiempo real en Power BI</span><span class="sxs-lookup"><span data-stu-id="c343a-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="c343a-204">En función de las opciones de Hola que desee configurar, asegúrese de que se primera [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) o [crear un concentrador de eventos Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="c343a-205">A continuación, seleccione opciones de Hola para donde desea que los datos de diagnóstico de toosend:</span><span class="sxs-lookup"><span data-stu-id="c343a-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Enviar datos tooAzure almacenamiento cuenta o evento de un centro](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="c343a-207">Períodos de retención se aplican únicamente cuando elija toouse una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c343a-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="c343a-208">Configuración de alertas de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="c343a-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="c343a-209">toomonitor determinadas métricas o superados umbrales para la aplicación lógica, configurar [alertas en Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="c343a-210">Más información sobre [métricas de Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c343a-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="c343a-211">tooset las alertas sin [Azure Log Analytics](../log-analytics/log-analytics-overview.md), siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c343a-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="c343a-212">Para usar criterios y acciones de alerta más avanzados, [configure Log Analytics](#azure-diagnostics) también.</span><span class="sxs-lookup"><span data-stu-id="c343a-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="c343a-213">En el menú de hoja de la aplicación de lógica hello, en **supervisión**, elija **diagnósticos** > **reglas de alerta** > **Agregar alerta**tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="c343a-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Adición de una alerta de la aplicación lógica](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="c343a-215">En hello **agregar una regla de alerta** hoja, crear la alerta, como se muestra:</span><span class="sxs-lookup"><span data-stu-id="c343a-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="c343a-216">En **Recurso**, seleccione la aplicación lógica si aún no está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c343a-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="c343a-217">Proporcione un nombre y una descripción para la alerta.</span><span class="sxs-lookup"><span data-stu-id="c343a-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="c343a-218">Seleccione un **métrica** o evento que desee tootrack.</span><span class="sxs-lookup"><span data-stu-id="c343a-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="c343a-219">Seleccione un **condición**, especifique un **umbral** de métrica de Hola y Hola seleccione **período** para la supervisión de esta métrica.</span><span class="sxs-lookup"><span data-stu-id="c343a-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="c343a-220">Seleccione si toosend de correo de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="c343a-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="c343a-221">Especificar ninguna otra dirección de correo electrónico para enviar alerta Hola.</span><span class="sxs-lookup"><span data-stu-id="c343a-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="c343a-222">También puede especificar una dirección URL del webhook que desee toosend Hola alert.</span><span class="sxs-lookup"><span data-stu-id="c343a-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="c343a-223">Por ejemplo, esta regla envía una alerta cuando hay errores en cinco o más ejecuciones en una hora:</span><span class="sxs-lookup"><span data-stu-id="c343a-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Creación de regla de alerta de métrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="c343a-225">toorun una aplicación de la lógica de una alerta, puede incluir hello [desencadenador de solicitud](../connectors/connectors-native-reqres.md) en el flujo de trabajo, que le permite realizar tareas como en estos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="c343a-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="c343a-226">Registrar tooSlack</span><span class="sxs-lookup"><span data-stu-id="c343a-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="c343a-227">Enviar un texto</span><span class="sxs-lookup"><span data-stu-id="c343a-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="c343a-228">Agregar una cola de mensajes tooa</span><span class="sxs-lookup"><span data-stu-id="c343a-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="c343a-229">Configuración de eventos y detalles de Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c343a-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="c343a-230">Cada evento de diagnóstico incluye detalles acerca de la aplicación lógica y ese evento, por ejemplo, el estado de hello, hora de inicio, hora de finalización y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="c343a-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="c343a-231">tooprogrammatically configurar la supervisión, el seguimiento y registro, unidad organizativa puede usar estos detalles con hello [API de REST para aplicaciones de Azure lógica](https://docs.microsoft.com/rest/api/logic) hello y [API de REST para diagnósticos de Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="c343a-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="c343a-232">Por ejemplo, hello `ActionCompleted` evento tiene hello `clientTrackingId` y `trackedProperties` propiedades que puede usar para el seguimiento y supervisión:</span><span class="sxs-lookup"><span data-stu-id="c343a-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

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

* <span data-ttu-id="c343a-233">`clientTrackingId`: Si no siempre, Azure genera este Id. y correlaciona eventos a través de una aplicación de lógica que se ejecuta automáticamente, incluidos los flujos de trabajo anidados que se denominan de aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="c343a-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="c343a-234">Puede especificar manualmente este Id. de un desencadenador pasando un `x-ms-client-tracking-id` encabezado con el valor de identificador personalizado en la solicitud de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="c343a-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="c343a-235">Puede usar un desencadenador de solicitud, un desencadenador HTTP o un desencadenador de webhook.</span><span class="sxs-lookup"><span data-stu-id="c343a-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="c343a-236">`trackedProperties`: tootrack entradas o salidas en datos de diagnóstico, puede agregar propiedades sometidas a seguimiento tooactions en definición de JSON de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c343a-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="c343a-237">Pueden realizar un seguimiento de propiedades sometidas a seguimiento únicamente una sola acción entradas y salidas, pero puede usar hello `correlation` propiedades de toocorrelate de eventos a través de acciones en una ejecución.</span><span class="sxs-lookup"><span data-stu-id="c343a-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="c343a-238">tootrack una o varias propiedades, agregar hello `trackedProperties` hello y sección propiedades que desee toohello definición de acción.</span><span class="sxs-lookup"><span data-stu-id="c343a-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="c343a-239">Por ejemplo, imagine que desea tootrack datos como un "identificador de pedido" en la telemetría:</span><span class="sxs-lookup"><span data-stu-id="c343a-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c343a-240">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c343a-240">Next steps</span></span>

* [<span data-ttu-id="c343a-241">Creación de plantillas para administrar la implementación y liberación de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="c343a-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="c343a-242">Escenarios B2B y comunicación con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="c343a-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="c343a-243">Supervisión de mensajes B2B</span><span class="sxs-lookup"><span data-stu-id="c343a-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)