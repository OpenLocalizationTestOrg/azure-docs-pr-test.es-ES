---
title: "aaaQuery para los mensajes B2B en Operations Management Suite: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: Crear consultas tootrack AS2, X 12 y EDIFACT mensajes de Hola Operations Management Suite
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="d6565-103">Consultar AS2, X 12 y EDIFACT mensajes de Hola Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="d6565-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="d6565-104">Hola toofind AS2, X 12 o mensajes EDIFACT que está realizando el seguimiento con [Azure Log Analytics](../log-analytics/log-analytics-overview.md) en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), puede crear consultas que filtran acciones basadas en específica criterios.</span><span class="sxs-lookup"><span data-stu-id="d6565-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="d6565-105">Por ejemplo, puede encontrar mensajes según un número de control de intercambio específico.</span><span class="sxs-lookup"><span data-stu-id="d6565-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="d6565-106">Requisitos</span><span class="sxs-lookup"><span data-stu-id="d6565-106">Requirements</span></span>

* <span data-ttu-id="d6565-107">Una aplicación lógica configurada con registro de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="d6565-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="d6565-108">Obtenga información acerca de [cómo una aplicación de la lógica de toocreate](../logic-apps/logic-apps-create-a-logic-app.md) y [cómo tooset el registro para esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="d6565-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="d6565-109">Una cuenta de integración configurada con supervisión y registro.</span><span class="sxs-lookup"><span data-stu-id="d6565-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="d6565-110">Obtenga información acerca de [cómo toocreate una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) y [cómo tooset supervisión y registro para esa cuenta](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="d6565-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="d6565-111">Si no lo ha hecho ya, [publicar datos de diagnóstico tooLog análisis](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) y [configurar el seguimiento de mensajes en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="d6565-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d6565-112">Después de que cumple los requisitos anteriores de hello, debe tener un área de trabajo en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6565-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="d6565-113">Debe usar Hola la misma área de trabajo OMS para realizar el seguimiento de la comunicación B2B de OMS.</span><span class="sxs-lookup"><span data-stu-id="d6565-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="d6565-114">Si no tiene un área de trabajo OMS, descubra [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6565-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="d6565-115">Crear consultas de mensaje con los filtros en el portal de Operations Management Suite Hola</span><span class="sxs-lookup"><span data-stu-id="d6565-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="d6565-116">En este ejemplo se muestra cómo puede buscar mensajes según su número de control de intercambio.</span><span class="sxs-lookup"><span data-stu-id="d6565-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="d6565-117">Si conoce el nombre del área de trabajo OMS, ir a página de inicio de área de trabajo de tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) e iniciar en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="d6565-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="d6565-118">De lo contrario, empiece en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="d6565-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="d6565-119">Hola [portal de Azure](https://portal.azure.com), elija **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="d6565-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="d6565-120">Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="d6565-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Búsqueda de Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="d6565-122">En **Log Analytics**, busque y seleccione el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="d6565-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selección del área de trabajo de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="d6565-124">En **Administración**, elija **Portal de OMS**.</span><span class="sxs-lookup"><span data-stu-id="d6565-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Selección de Portal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="d6565-126">En la página principal de OMS, seleccione **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="d6565-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="d6565-128">O bien</span><span class="sxs-lookup"><span data-stu-id="d6565-128">-or-</span></span>

   ![En el menú OMS de hello, elija "Búsqueda de registros"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="d6565-130">En el cuadro de búsqueda de hello, escriba un campo que desea que toofind y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="d6565-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="d6565-131">Cuando empiece a escribir, OMS le mostrará posibles coincidencias y operaciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="d6565-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="d6565-132">Obtenga más información sobre [cómo toofind datos de análisis de registros](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="d6565-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="d6565-133">En este ejemplo se buscan eventos con **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="d6565-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Empezar a escribir la cadena de consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="d6565-135">En la barra de la izquierda hello, elija el período de tiempo de Hola que desea tooview.</span><span class="sxs-lookup"><span data-stu-id="d6565-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="d6565-136">tooadd una consulta de tooyour filtro, elija **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="d6565-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Agregar filtro tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="d6565-138">En **agregar filtros**, escriba el nombre de filtro de Hola para que pueda encontrar el filtro de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="d6565-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="d6565-139">Seleccione el filtro de Hola y elija **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="d6565-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="d6565-140">número de control de intercambio de hello toofind, este ejemplo busca palabra Hola "intercambio" y selecciona **event_record_messageProperties_interchangeControlNumber_s** como filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6565-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Selección de filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="d6565-142">En la barra de la izquierda hello, seleccione el valor de filtro de Hola que desee toouse y elija **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d6565-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="d6565-143">Este ejemplo selecciona el número de control de intercambio de Hola para los mensajes de Hola que deseamos.</span><span class="sxs-lookup"><span data-stu-id="d6565-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Selección de valor de filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="d6565-145">Consulta de toohello devuelven ahora que va a compilar.</span><span class="sxs-lookup"><span data-stu-id="d6565-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="d6565-146">La consulta se actualizó con el valor y el evento de filtro seleccionados.</span><span class="sxs-lookup"><span data-stu-id="d6565-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="d6565-147">Los resultados anteriores también se filtraron.</span><span class="sxs-lookup"><span data-stu-id="d6565-147">Your previous results are now filtered too.</span></span>

    ![Devolver tooyour consulta con los resultados filtrados](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="d6565-149">Guardar la consulta para futuro uso</span><span class="sxs-lookup"><span data-stu-id="d6565-149">Save your query for future use</span></span>

1. <span data-ttu-id="d6565-150">De la consulta en hello **Log Search** página, elija **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d6565-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="d6565-151">Asigne un nombre a la consulta, seleccione una categoría y elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d6565-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Asignación de nombre y categoría a la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="d6565-153">tooview la consulta, elija **favoritos**.</span><span class="sxs-lookup"><span data-stu-id="d6565-153">tooview your query, choose **Favorites**.</span></span>

   ![Elegir "Favoritos"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="d6565-155">En **búsquedas guardadas**, seleccione la consulta para que pueda ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6565-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="d6565-156">consulta de hello tooupdate para que pueda encontrar resultados diferentes, en Editar consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="d6565-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Selección de la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="d6565-158">Buscar y ejecutar las consultas guardadas en el portal de Operations Management Suite Hola</span><span class="sxs-lookup"><span data-stu-id="d6565-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="d6565-159">Abra la página principal del área de trabajo de OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) y elija **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="d6565-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="d6565-161">O bien</span><span class="sxs-lookup"><span data-stu-id="d6565-161">-or-</span></span>

   ![En el menú OMS de hello, elija "Búsqueda de registros"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="d6565-163">En hello **Log Search** página principal, elija **favoritos**.</span><span class="sxs-lookup"><span data-stu-id="d6565-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![Elegir "Favoritos"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="d6565-165">En **búsquedas guardadas**, seleccione la consulta para que pueda ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6565-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="d6565-166">consulta de hello tooupdate para que pueda encontrar resultados diferentes, en Editar consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="d6565-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Selección de la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="d6565-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6565-168">Next steps</span></span>

* [<span data-ttu-id="d6565-169">Esquemas de seguimiento de AS2</span><span class="sxs-lookup"><span data-stu-id="d6565-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="d6565-170">Esquemas de seguimiento de X12</span><span class="sxs-lookup"><span data-stu-id="d6565-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="d6565-171">Esquemas de seguimiento personalizados</span><span class="sxs-lookup"><span data-stu-id="d6565-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)