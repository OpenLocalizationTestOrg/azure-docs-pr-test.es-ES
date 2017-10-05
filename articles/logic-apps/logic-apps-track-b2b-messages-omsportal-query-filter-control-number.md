---
title: Consulta de mensajes B2B en Operations Management Suite - Azure Logic Apps | Microsoft Docs
description: Cree consultas para hacer seguimiento de los mensajes AS2, X12 y EDIFACT en Operations Management Suite
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
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="ed846-103">Consulta de mensajes AS2, X12 y EDIFACT en Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="ed846-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="ed846-104">Para encontrar los mensajes AS2, X12 o EDIFACT a los que hace seguimiento con [Azure Log Analytics](../log-analytics/log-analytics-overview.md) en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), puede crear consultas que filtren las acciones según criterios específicos.</span><span class="sxs-lookup"><span data-stu-id="ed846-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="ed846-105">Por ejemplo, puede encontrar mensajes según un número de control de intercambio específico.</span><span class="sxs-lookup"><span data-stu-id="ed846-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="ed846-106">Requisitos</span><span class="sxs-lookup"><span data-stu-id="ed846-106">Requirements</span></span>

* <span data-ttu-id="ed846-107">Una aplicación lógica configurada con registro de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="ed846-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="ed846-108">Obtenga información sobre [cómo crear una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) y [cómo configurar el registro de esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="ed846-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="ed846-109">Una cuenta de integración configurada con supervisión y registro.</span><span class="sxs-lookup"><span data-stu-id="ed846-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="ed846-110">Obtenga información sobre [cómo crear una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) y [cómo configurar la supervisión y el registro de esa cuenta](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="ed846-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="ed846-111">Si aún no lo ha hecho, [publique datos de diagnóstico para Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) y [establezca el seguimiento de mensajes en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="ed846-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ed846-112">Después de haber satisfecho los requisitos anteriores, debería tener un área de trabajo en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed846-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="ed846-113">Debería usar la misma área de trabajo de OMS para realizar el seguimiento de la comunicación B2B en OMS.</span><span class="sxs-lookup"><span data-stu-id="ed846-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="ed846-114">Si no tiene un área de trabajo de OMS, aprenda a [crear un área de trabajo de OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed846-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="ed846-115">Creación de consultas de mensajes con filtros en el portal de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="ed846-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="ed846-116">En este ejemplo se muestra cómo puede buscar mensajes según su número de control de intercambio.</span><span class="sxs-lookup"><span data-stu-id="ed846-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="ed846-117">Si conoce el nombre del área de trabajo de OMS, vaya a la página principal del área de trabajo (`https://{your-workspace-name}.portal.mms.microsoft.com`) y empiece en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="ed846-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="ed846-118">De lo contrario, empiece en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="ed846-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="ed846-119">En [Azure Portal](https://portal.azure.com), elija **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="ed846-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="ed846-120">Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="ed846-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Búsqueda de Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="ed846-122">En **Log Analytics**, busque y seleccione el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="ed846-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selección del área de trabajo de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="ed846-124">En **Administración**, elija **Portal de OMS**.</span><span class="sxs-lookup"><span data-stu-id="ed846-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Selección de Portal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="ed846-126">En la página principal de OMS, seleccione **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="ed846-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="ed846-128">O bien</span><span class="sxs-lookup"><span data-stu-id="ed846-128">-or-</span></span>

   ![Selección de "Búsqueda de registros" en el menú OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="ed846-130">En el cuadro de búsqueda, especifique un campo que quiera buscar y pulse **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="ed846-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="ed846-131">Cuando empiece a escribir, OMS le mostrará posibles coincidencias y operaciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="ed846-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="ed846-132">Más información sobre [cómo buscar datos en Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="ed846-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="ed846-133">En este ejemplo se buscan eventos con **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="ed846-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Empezar a escribir la cadena de consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="ed846-135">En la barra de la izquierda, elija el período de tiempo que desea consultar.</span><span class="sxs-lookup"><span data-stu-id="ed846-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="ed846-136">Para agregar un filtro a la consulta, elija **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ed846-136">To add a filter to your query, choose **+Add**.</span></span>

   ![Agregar filtro a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="ed846-138">En **Agregar filtros**, escriba el nombre del filtro para poder encontrar el que quiere.</span><span class="sxs-lookup"><span data-stu-id="ed846-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="ed846-139">Seleccione el filtro y elija **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ed846-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="ed846-140">Para buscar el número de control de intercambio, este ejemplo busca la palabra "intercambio" y selecciona **event_record_messageProperties_interchangeControlNumber_s** como filtro.</span><span class="sxs-lookup"><span data-stu-id="ed846-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![Selección de filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="ed846-142">En la barra de la izquierda, seleccione el valor de filtro que quiere usar y elija **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ed846-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="ed846-143">En este ejemplo se selecciona el número de control de intercambio para los mensajes que deseamos.</span><span class="sxs-lookup"><span data-stu-id="ed846-143">This example selects the interchange control number for the messages we want.</span></span>

   ![Selección de valor de filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="ed846-145">Ahora vuelva a la consulta que está creando.</span><span class="sxs-lookup"><span data-stu-id="ed846-145">Now return to the query that you're building.</span></span> <span data-ttu-id="ed846-146">La consulta se actualizó con el valor y el evento de filtro seleccionados.</span><span class="sxs-lookup"><span data-stu-id="ed846-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="ed846-147">Los resultados anteriores también se filtraron.</span><span class="sxs-lookup"><span data-stu-id="ed846-147">Your previous results are now filtered too.</span></span>

    ![Consulta con los resultados filtrados](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="ed846-149">Guardar la consulta para futuro uso</span><span class="sxs-lookup"><span data-stu-id="ed846-149">Save your query for future use</span></span>

1. <span data-ttu-id="ed846-150">Desde la consulta en la página **Búsqueda de registros**, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed846-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="ed846-151">Asigne un nombre a la consulta, seleccione una categoría y elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed846-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Asignación de nombre y categoría a la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="ed846-153">Para ver la consulta, elija **Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="ed846-153">To view your query, choose **Favorites**.</span></span>

   ![Elegir "Favoritos"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="ed846-155">En **Búsquedas guardadas**, seleccione la consulta para poder ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="ed846-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="ed846-156">Edite la consulta para actualizarla y poder encontrar distintos resultados.</span><span class="sxs-lookup"><span data-stu-id="ed846-156">To update the query so you can find different results, edit the query.</span></span>

   ![Selección de la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="ed846-158">Búsqueda y ejecución de consultas guardadas en el portal de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="ed846-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="ed846-159">Abra la página principal del área de trabajo de OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) y elija **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="ed846-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="ed846-161">O bien</span><span class="sxs-lookup"><span data-stu-id="ed846-161">-or-</span></span>

   ![Selección de "Búsqueda de registros" en el menú OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="ed846-163">En la página principal de **Búsqueda de registros**, elija **Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="ed846-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![Elegir "Favoritos"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="ed846-165">En **Búsquedas guardadas**, seleccione la consulta para poder ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="ed846-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="ed846-166">Edite la consulta para actualizarla y poder encontrar distintos resultados.</span><span class="sxs-lookup"><span data-stu-id="ed846-166">To update the query so you can find different results, edit the query.</span></span>

   ![Selección de la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="ed846-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed846-168">Next steps</span></span>

* [<span data-ttu-id="ed846-169">Esquemas de seguimiento de AS2</span><span class="sxs-lookup"><span data-stu-id="ed846-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="ed846-170">Esquemas de seguimiento de X12</span><span class="sxs-lookup"><span data-stu-id="ed846-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="ed846-171">Esquemas de seguimiento personalizados</span><span class="sxs-lookup"><span data-stu-id="ed846-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)