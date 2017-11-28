---
title: "aaaMonitor y obtener información acerca de la lógica de aplicación se ejecuta con OMS - Azure Logic Apps | Documentos de Microsoft"
description: "Supervisar se ejecuta la aplicación lógica con visión tooget de análisis de registros y Operations Management Suite (OMS) y los detalles de depuración más enriquecidas para solución de problemas y diagnóstico"
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
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="c6b40-103">Supervise y obtenga información sobre las ejecuciones de aplicación lógica con Operations Management Suite (OMS) y Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6b40-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="c6b40-104">Para obtener información de depuración más enriquecida y supervisión, puede activar el análisis de registros en hello vez cuando se crea una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="c6b40-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="c6b40-105">Análisis de registros proporciona supervisión para la aplicación lógica y el registro de diagnóstico se ejecuta a través del portal de hello Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="c6b40-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="c6b40-106">Cuando se agrega tooOMS de solución de administración de aplicaciones de la lógica de hello, puede ver el estado agregado para sus ejecuciones de aplicación lógica y los detalles específicos como estado, tiempo de ejecución, estado de reenvío y el identificador de correlación.</span><span class="sxs-lookup"><span data-stu-id="c6b40-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="c6b40-107">Este tema muestra cómo tooturn en análisis de registros o instale Hola solución de administración de aplicaciones de la lógica de OMS por lo que puede ver los eventos en tiempo de ejecución y los datos para la aplicación lógica de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="c6b40-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="c6b40-108">toomonitor sus aplicaciones existentes de lógica, siga estos pasos demasiado [activar registro de diagnóstico y enviar tooOMS de datos de tiempo de ejecución de aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="c6b40-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="c6b40-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="c6b40-109">Requirements</span></span>

<span data-ttu-id="c6b40-110">Antes de empezar, deberá toohave un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="c6b40-111">Obtenga información acerca de [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6b40-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="c6b40-112">Activación del registro de diagnóstico al crear aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="c6b40-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="c6b40-113">En [Azure Portal](https://portal.azure.com), cree una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c6b40-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="c6b40-114">Elija **Nueva** > **Enterprise Integration** > **Aplicación lógica** > **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Creación de una aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="c6b40-116">Hola **crear lógica aplicación** página, lleve a cabo estas tareas como se muestra:</span><span class="sxs-lookup"><span data-stu-id="c6b40-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="c6b40-117">Asigne un nombre a la aplicación lógica y seleccione su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b40-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="c6b40-118">Cree o seleccione un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b40-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="c6b40-119">Establecer **análisis de registros** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="c6b40-120">Área de trabajo OMS de hello SELECT en la que desea enviar demasiado datos para la aplicación lógica se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="c6b40-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="c6b40-121">Cuando esté listo, elija **Pin toodashboard** > **crear**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Creación de la aplicación lógica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="c6b40-123">Después de realizar este paso, Azure crea la aplicación lógica, que ahora está asociada al área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="c6b40-124">Además, este paso también instala automáticamente soluciones de administración de aplicaciones de la lógica de hello en el área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="c6b40-125">tooview se ejecuta la aplicación de lógica de OMS, [continúe con estos pasos](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="c6b40-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="c6b40-126">Instalar la solución de administración de aplicaciones de la lógica de Hola de OMS</span><span class="sxs-lookup"><span data-stu-id="c6b40-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="c6b40-127">Si ya activó Log Analytics cuando creó su aplicación lógica, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="c6b40-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="c6b40-128">Ya tiene instalada en OMS de solución de administración de aplicaciones de la lógica de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b40-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="c6b40-129">Hola [portal de Azure](https://portal.azure.com), elija **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c6b40-130">Busque "log analytics" como filtro y elija **Log Analytics** como se muestra:</span><span class="sxs-lookup"><span data-stu-id="c6b40-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Selección de "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="c6b40-132">En **Log Analytics**, busque y seleccione el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selección del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="c6b40-134">En **Administración**, elija **Portal de OMS**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Selección de "Portal de OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="c6b40-136">En la página principal OMS, si aparece el banner de actualización de hello, elija pancarta Hola para que primero actualizan el área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="c6b40-137">A continuación, elija **Galería de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-137">Then choose **Solutions Gallery**.</span></span>

   ![Selección de "Galería de soluciones"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="c6b40-139">En **todas las soluciones**, buscar y elija el icono de Hola para hello **lógica de administración de aplicaciones** solución.</span><span class="sxs-lookup"><span data-stu-id="c6b40-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Selección de "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="c6b40-141">solución de hello tooinstall en el área de trabajo OMS, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Selección de "Agregar" en "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="c6b40-143">Visualización de ejecuciones de aplicación lógica en el área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="c6b40-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="c6b40-144">recuento de hello tooview y el estado de la aplicación lógica se ejecuta, vaya toohello página de información general para el área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="c6b40-145">Revise los detalles de hello en hello **lógica de administración de aplicaciones** icono.</span><span class="sxs-lookup"><span data-stu-id="c6b40-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Icono de información general que muestra el recuento y el estado de la ejecución de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="c6b40-147">Si esta actualización pancarta aparece en lugar de icono de administración de aplicaciones de lógica de hello, elija pancarta Hola para que primero actualizan el área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="c6b40-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Actualización del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="c6b40-149">tooview un resumen con más detalles acerca de cómo se ejecuta la aplicación de lógica, elija hello **lógica de administración de aplicaciones** icono.</span><span class="sxs-lookup"><span data-stu-id="c6b40-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="c6b40-150">En este caso, las ejecuciones de aplicación lógica se agrupan por nombre y estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c6b40-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Resumen de estado de las ejecuciones de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="c6b40-152">tooview que Hola a todos se ejecuta para una aplicación lógica específica o el estado, la fila de hello select para una aplicación de lógica o con el estado.</span><span class="sxs-lookup"><span data-stu-id="c6b40-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="c6b40-153">Este es un ejemplo que muestra todas las ejecuciones de Hola para una aplicación de la lógica específica:</span><span class="sxs-lookup"><span data-stu-id="c6b40-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Visualización de las ejecuciones de una aplicación lógica o el estado](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="c6b40-155">Hola **reenvío** columna muestra "Sí" para las ejecuciones que son el resultado de una ejecución reenviada.</span><span class="sxs-lookup"><span data-stu-id="c6b40-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="c6b40-156">toofilter estos resultados, puede realizar un filtrado de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="c6b40-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="c6b40-157">El filtro del lado cliente: para cada columna, elija los filtros de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="c6b40-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="c6b40-158">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="c6b40-158">Here are some examples:</span></span>

     ![Ejemplo de filtros de columna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="c6b40-160">Filtro de servidor: toochoose un hora específica ventana o toolimit Hola el número de ejecuciones que aparecen, usar el control del ámbito de hello al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b40-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="c6b40-161">De forma predeterminada, solo aparecen 1000 registros a la vez.</span><span class="sxs-lookup"><span data-stu-id="c6b40-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Cambio de ventana de tiempo de Hola](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="c6b40-163">tooview todos los Hola acciones y sus detalles para una ejecución, específica, seleccione una fila, que abre la página de búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b40-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="c6b40-164">Esta información en una tabla, elija a tooview **tabla**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="c6b40-165">consulta de hello toochange, puede editar cadena de consulta de hello en la barra de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b40-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="c6b40-166">Para una mejor experiencia, elija **Análisis avanzado**.</span><span class="sxs-lookup"><span data-stu-id="c6b40-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Visualización de las acciones y los detalles de una ejecución de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="c6b40-168">Aquí en la página de análisis de registros de Azure de hello, puede actualizar las consultas y vista Hola resultante de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b40-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="c6b40-169">Esta consulta utiliza [lenguaje de consulta de Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que se puede modificar si desea que los resultados diferentes tooview.</span><span class="sxs-lookup"><span data-stu-id="c6b40-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics: vista de consultas](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="c6b40-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6b40-171">Next steps</span></span>

* [<span data-ttu-id="c6b40-172">Supervisión de mensajes B2B</span><span class="sxs-lookup"><span data-stu-id="c6b40-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
