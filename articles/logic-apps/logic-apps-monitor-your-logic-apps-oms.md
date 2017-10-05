---
title: "Supervisión y obtención de información sobre las ejecuciones de aplicación lógica mediante OMS: Azure Logic Apps | Microsoft Docs"
description: "Supervise sus ejecuciones de aplicación lógica con Log Analytics y Operations Management Suite (OMS) para obtener información y detalles de depuración más abundantes de cara a la solución de problemas y el diagnóstico."
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="6657a-103">Supervise y obtenga información sobre las ejecuciones de aplicación lógica con Operations Management Suite (OMS) y Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6657a-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="6657a-104">Para realizar la supervisión y obtener información de depuración abundante, puede activar Log Analytics al mismo tiempo que crea una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="6657a-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="6657a-105">Log Analytics proporciona registro de diagnóstico y supervisión de las ejecuciones de aplicación lógica mediante el portal de Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="6657a-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="6657a-106">Cuando se agrega la solución Logic Apps Management a OMS, se obtiene el estado agregado de las ejecuciones de aplicación lógica, junto con detalles específicos, como el estado, el tiempo de ejecución, el estado de reenvío y los id. de correlación.</span><span class="sxs-lookup"><span data-stu-id="6657a-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="6657a-107">En este tema se muestra cómo activar Log Analytics o instalar la solución Logic Apps Management en OMS, de modo que pueda ver eventos y datos en tiempo de ejecución de sus ejecuciones de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="6657a-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="6657a-108">Para supervisar las aplicaciones lógicas existentes, siga estos pasos para [activar el registro de diagnóstico y enviar datos de tiempo de ejecución de aplicaciones lógicas a OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="6657a-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="6657a-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="6657a-109">Requirements</span></span>

<span data-ttu-id="6657a-110">Antes de empezar, necesita un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="6657a-111">Aprenda [cómo crear un área de trabajo de OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6657a-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="6657a-112">Activación del registro de diagnóstico al crear aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="6657a-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="6657a-113">En [Azure Portal](https://portal.azure.com), cree una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="6657a-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="6657a-114">Elija **Nueva** > **Enterprise Integration** > **Aplicación lógica** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6657a-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Creación de una aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="6657a-116">En la página **Crear aplicación lógica**, realice estas tareas de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="6657a-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="6657a-117">Asigne un nombre a la aplicación lógica y seleccione su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6657a-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="6657a-118">Cree o seleccione un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6657a-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="6657a-119">Establezca **Log Analytics** en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="6657a-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="6657a-120">Seleccione el área de trabajo de OMS donde desea enviar los datos de las ejecuciones de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="6657a-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="6657a-121">Cuando esté listo, elija **Anclar al panel** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6657a-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Creación de la aplicación lógica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="6657a-123">Después de realizar este paso, Azure crea la aplicación lógica, que ahora está asociada al área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="6657a-124">Además, este paso también instala automáticamente la solución Logic Apps Management en el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="6657a-125">Para ver las ejecuciones de aplicación lógica en OMS, [continúe con estos pasos](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="6657a-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="6657a-126">Instalación de la solución Logic Apps Management en OMS</span><span class="sxs-lookup"><span data-stu-id="6657a-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="6657a-127">Si ya activó Log Analytics cuando creó su aplicación lógica, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="6657a-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="6657a-128">Ya tiene instalada la solución Logic Apps Management en OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="6657a-129">En [Azure Portal](https://portal.azure.com), elija **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="6657a-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="6657a-130">Busque "log analytics" como filtro y elija **Log Analytics** como se muestra:</span><span class="sxs-lookup"><span data-stu-id="6657a-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Selección de "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="6657a-132">En **Log Analytics**, busque y seleccione el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selección del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="6657a-134">En **Administración**, elija **Portal de OMS**.</span><span class="sxs-lookup"><span data-stu-id="6657a-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Selección de "Portal de OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="6657a-136">En la página principal de OMS, si aparece el banner de actualización, elíjalo para actualizar primero el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="6657a-137">A continuación, elija **Galería de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="6657a-137">Then choose **Solutions Gallery**.</span></span>

   ![Selección de "Galería de soluciones"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="6657a-139">En **Todas las soluciones**, busque y elija el icono de la solución **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="6657a-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   ![Selección de "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="6657a-141">Para instalar la solución en el área de trabajo de OMS, elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6657a-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   ![Selección de "Agregar" en "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="6657a-143">Visualización de ejecuciones de aplicación lógica en el área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="6657a-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="6657a-144">Para ver el recuento y el estado de las ejecuciones de aplicación lógica, vaya a la página de información general del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="6657a-145">Revise los detalles del icono **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="6657a-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Icono de información general que muestra el recuento y el estado de la ejecución de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="6657a-147">Si en lugar del icono de Logic Apps Management aparece este banner de actualización, elíjalo para actualizar primero el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="6657a-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Actualización del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="6657a-149">Para ver un resumen con más detalles sobre las ejecuciones de aplicación lógica, elija el icono **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="6657a-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="6657a-150">En este caso, las ejecuciones de aplicación lógica se agrupan por nombre y estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6657a-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Resumen de estado de las ejecuciones de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="6657a-152">Para ver todas las ejecuciones de una aplicación lógica específica o el estado, seleccione la fila correspondiente a la aplicación lógica o el estado.</span><span class="sxs-lookup"><span data-stu-id="6657a-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="6657a-153">A continuación se muestra un ejemplo con todas las ejecuciones de una aplicación lógica específica:</span><span class="sxs-lookup"><span data-stu-id="6657a-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![Visualización de las ejecuciones de una aplicación lógica o el estado](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="6657a-155">La columna **Resubmission** (Reenvío) muestra "Sí" para todas las ejecuciones que resultan de una ejecución reenviada.</span><span class="sxs-lookup"><span data-stu-id="6657a-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="6657a-156">Para filtrar estos resultados, puede realizar un filtrado en el cliente y en el servidor.</span><span class="sxs-lookup"><span data-stu-id="6657a-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="6657a-157">Filtro en el cliente: para cada columna, elija los filtros que prefiera.</span><span class="sxs-lookup"><span data-stu-id="6657a-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="6657a-158">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="6657a-158">Here are some examples:</span></span>

     ![Ejemplo de filtros de columna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="6657a-160">Filtro en el servidor: para elegir una ventana de tiempo específica o para limitar el número de ejecuciones que aparecen, use el control de ámbito de la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="6657a-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="6657a-161">De forma predeterminada, solo aparecen 1000 registros a la vez.</span><span class="sxs-lookup"><span data-stu-id="6657a-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Cambio de la ventana de tiempo](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="6657a-163">Para ver todas las acciones y sus detalles para una ejecución concreta, seleccione una fila y se abrirá la página de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="6657a-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="6657a-164">Para ver esta información en una tabla, elija **Tabla**.</span><span class="sxs-lookup"><span data-stu-id="6657a-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="6657a-165">Para cambiar la consulta, puede modificar la cadena de consulta en la barra de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6657a-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="6657a-166">Para una mejor experiencia, elija **Análisis avanzado**.</span><span class="sxs-lookup"><span data-stu-id="6657a-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Visualización de las acciones y los detalles de una ejecución de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="6657a-168">Aquí, en la página de Azure Log Analytics, puede actualizar las consultas y ver los resultados de la tabla.</span><span class="sxs-lookup"><span data-stu-id="6657a-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="6657a-169">En esta consulta se usa el [lenguaje de consulta de Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que puede modificar si quiere ver resultados diferentes.</span><span class="sxs-lookup"><span data-stu-id="6657a-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Azure Log Analytics: vista de consultas](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="6657a-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6657a-171">Next steps</span></span>

* [<span data-ttu-id="6657a-172">Supervisión de mensajes B2B</span><span class="sxs-lookup"><span data-stu-id="6657a-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
