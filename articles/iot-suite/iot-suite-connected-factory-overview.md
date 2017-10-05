---
title: "Información general de la fábrica conectada del Conjunto de aplicaciones de IoT de Azure | Microsoft Docs"
description: "Descripción de la solución preconfigurada de fábrica conectada del Conjunto de aplicaciones de IoT de Azure."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="99c2d-103">Introducción a la solución preconfigurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="99c2d-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="99c2d-104">Las [soluciones preconfiguradas][lnk-preconfigured-solutions] del Conjunto de aplicaciones de IoT de Azure combinan varios servicios de IoT de Azure para ofrecer soluciones integrales que implementan escenarios empresariales de IoT comunes.</span><span class="sxs-lookup"><span data-stu-id="99c2d-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="99c2d-105">La solución preconfigurada *fábrica conectada* permite conectar y supervisar dispositivos industriales.</span><span class="sxs-lookup"><span data-stu-id="99c2d-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="99c2d-106">Puede usar la solución para analizar el flujo de datos de los dispositivos y administrar la productividad y la rentabilidad de las operaciones.</span><span class="sxs-lookup"><span data-stu-id="99c2d-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="99c2d-107">Este tutorial muestra cómo aprovisionar la solución preconfigurada de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="99c2d-108">También le guía por las características básicas de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="99c2d-109">Puede acceder a muchas de estas características desde el *panel* de soluciones que se implementa como parte de la solución preconfigurada:</span><span class="sxs-lookup"><span data-stu-id="99c2d-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![panel de la solución preconfigurada de fábrica conectada][img-cf-home]

<span data-ttu-id="99c2d-111">Para completar este tutorial, deberá tener una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="99c2d-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="99c2d-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="99c2d-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="99c2d-113">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="99c2d-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="99c2d-114">Aprovisionamiento de la solución</span><span class="sxs-lookup"><span data-stu-id="99c2d-114">Provision the solution</span></span>

1. <span data-ttu-id="99c2d-115">Inicie sesión en azureiotsuite.com con sus credenciales de la cuenta de Azure y haga clic en "**+**" para crear una solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="99c2d-116">Haga clic en **Seleccionar** en el icono **Fábrica conectada**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="99c2d-117">Escriba un valor en **Nombre de la solución** para la solución preconfigurada de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="99c2d-118">Seleccione la **Suscripción** y **Región** que desea usar para aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="99c2d-119">Haga clic en **Crear solución** para comenzar el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="99c2d-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="99c2d-120">Este proceso normalmente tarda varios minutos en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="99c2d-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="99c2d-121">Mientras espera a que se complete el proceso de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="99c2d-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="99c2d-122">Haga clic en el icono de la solución con el estado **Aprovisionando**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="99c2d-123">Observe los **estados de aprovisionamiento** , ya que los servicios de Azure se implementan en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="99c2d-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="99c2d-124">Una vez que se complete el aprovisionamiento, el estado cambia a **Listo**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="99c2d-125">Haga clic en el icono y verá los detalles de la solución en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="99c2d-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="99c2d-126">Si surgen problemas al implementar la solución preconfigurada, revise las secciones [Permisos en el sitio azureiotsuite.com][lnk-permissions] y [Preguntas frecuentes sobre la fábrica conectada](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="99c2d-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="99c2d-127">Si los problemas persisten, cree un vale de servicio en el [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="99c2d-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="99c2d-128">¿Hay detalles que esperaría ver que no aparezcan para su solución?</span><span class="sxs-lookup"><span data-stu-id="99c2d-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="99c2d-129">Puede sugerirnos nuevas características en [User Voice](https://feedback.azure.com/forums/321918-azure-iot)(La voz del usuario).</span><span class="sxs-lookup"><span data-stu-id="99c2d-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="99c2d-130">Información general de escenario</span><span class="sxs-lookup"><span data-stu-id="99c2d-130">Scenario overview</span></span>

<span data-ttu-id="99c2d-131">Al implementar la solución preconfigurada de fábrica conectada, esta se rellena previamente con los recursos que le permiten recorrer un escenario industrial común.</span><span class="sxs-lookup"><span data-stu-id="99c2d-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="99c2d-132">En este escenario, varias fábricas conectadas a la solución informan de los valores de datos necesarios para calcular la eficiencia general de los equipos (OEE) y los indicadores clave de rendimiento (KPI).</span><span class="sxs-lookup"><span data-stu-id="99c2d-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="99c2d-133">Las secciones siguientes le indicarán cómo:</span><span class="sxs-lookup"><span data-stu-id="99c2d-133">The following sections show you how to:</span></span>

* <span data-ttu-id="99c2d-134">Supervisar los valores de la fábrica, las líneas de producción, el valor de OEE de las estaciones y los valores de KPI</span><span class="sxs-lookup"><span data-stu-id="99c2d-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="99c2d-135">Analizar los datos de telemetría generados por estos dispositivos con Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="99c2d-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="99c2d-136">Actuar sobre las alertas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="99c2d-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="99c2d-137">Una característica clave de este escenario es que se pueden realizar todas estas acciones de forma remota desde el panel de la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="99c2d-138">No es necesario el acceso físico a los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="99c2d-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="99c2d-139">Visualización del panel de soluciones</span><span class="sxs-lookup"><span data-stu-id="99c2d-139">View the solution dashboard</span></span>

<span data-ttu-id="99c2d-140">El panel de la solución permite administrar la solución implementada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="99c2d-141">Es una representación jerárquica de una configuración de fábrica global.</span><span class="sxs-lookup"><span data-stu-id="99c2d-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="99c2d-142">Por ejemplo, puede ver los valores de OEE y KPI, publicar nuevos nodos para telemetría y actuar sobre las alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="99c2d-143">Cuando se haya completado el aprovisionamiento y el icono de la solución preconfigurada indique **Listo**, seleccione **Iniciar** para abrir el portal de la solución de fábrica conectada en una nueva pestaña.</span><span class="sxs-lookup"><span data-stu-id="99c2d-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![Iniciar la solución preconfigurada][img-launch-solution]

1. <span data-ttu-id="99c2d-145">De forma predeterminada, el portal de la solución muestra el *panel*.</span><span class="sxs-lookup"><span data-stu-id="99c2d-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="99c2d-146">Use el menú del lado izquierdo de la página para navegar a otras áreas del portal.</span><span class="sxs-lookup"><span data-stu-id="99c2d-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![Panel de la solución preconfigurada de fábrica conectada][cf-img-menu]

<span data-ttu-id="99c2d-148">El panel muestra la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="99c2d-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="99c2d-149">Un panel **Lista de fábricas** que muestra el estado, la ubicación y la configuración actual de producción de la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="99c2d-150">La primera vez que se ejecuta la solución hay una serie de dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="99c2d-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="99c2d-151">La simulación de la línea de producción se compone de tres servidores OPC UA reales por línea de producción que realizan tareas simuladas y comparten datos.</span><span class="sxs-lookup"><span data-stu-id="99c2d-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="99c2d-152">Para más información acerca de OPC UA, consulte las [preguntas frecuentes sobre la fábrica conectada](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="99c2d-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="99c2d-153">Un **mapa** que muestra la ubicación de cada dispositivo conectado a la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="99c2d-154">La solución puede utilizar la API de Bing Maps para trazar la información en el mapa.</span><span class="sxs-lookup"><span data-stu-id="99c2d-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="99c2d-155">Si la suscripción está habilitada para la API de Bing Maps Enterprise, esta característica se usa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="99c2d-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="99c2d-156">Si no es así, consulte las [preguntas más frecuentes][lnk-faq] para obtener información sobre cómo hacer que el mapa se vuelva dinámico.</span><span class="sxs-lookup"><span data-stu-id="99c2d-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="99c2d-157">Un panel de **Alertas**, que muestra las alertas generadas cuando un valor de OEE, KPI o telemetría supera un umbral específico.</span><span class="sxs-lookup"><span data-stu-id="99c2d-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="99c2d-158">Un panel **Eficiencia general de los equipos** que muestra los valores de OEE para toda la empresa o para la fábrica, línea de producción o estación que esté visualizando.</span><span class="sxs-lookup"><span data-stu-id="99c2d-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="99c2d-159">Este valor se agrega desde la vista de estación hasta el nivel de empresa.</span><span class="sxs-lookup"><span data-stu-id="99c2d-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="99c2d-160">La cifra de OEE y sus elementos constituyentes se pueden analizar aún más.</span><span class="sxs-lookup"><span data-stu-id="99c2d-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="99c2d-161">Un panel de **Indicadores clave de rendimiento** que muestra el número de unidades producidas y energía usada por toda la empresa o por la fábrica, línea de producción o estación que esté visualizando.</span><span class="sxs-lookup"><span data-stu-id="99c2d-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="99c2d-162">Estos valores se agregan desde la vista de estación hasta el nivel de empresa.</span><span class="sxs-lookup"><span data-stu-id="99c2d-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="99c2d-163">Visualización de fábricas</span><span class="sxs-lookup"><span data-stu-id="99c2d-163">View factories</span></span>

<span data-ttu-id="99c2d-164">El panel *Fábricas* muestra la ubicación geográfica de todas las fábricas incluidas en la solución, su estado y la configuración de producción actual.</span><span class="sxs-lookup"><span data-stu-id="99c2d-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="99c2d-165">En la lista de ubicaciones, puede navegar a los otros niveles de la jerarquía de la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="99c2d-166">Las filas de la lista son hipervínculos que vinculan los detalles de las líneas de producción en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="99c2d-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="99c2d-167">Así es posible profundizar en los detalles de la línea de producción y descender hasta la vista de estación.</span><span class="sxs-lookup"><span data-stu-id="99c2d-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="99c2d-168">También puede aplicar un filtro a la lista.</span><span class="sxs-lookup"><span data-stu-id="99c2d-168">You can also apply a filter to the list.</span></span>

![Fábricas de la solución preconfigurada de fábrica conectada][cf-img-factories] 

1. <span data-ttu-id="99c2d-170">El **panel Fábrica** muestra la lista de fábricas para esta solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="99c2d-171">La lista de fábricas muestra inicialmente seis fábricas creadas por el proceso de aprovisionamiento,</span><span class="sxs-lookup"><span data-stu-id="99c2d-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="99c2d-172">pero se pueden agregar más dispositivos simulados y físicos a la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="99c2d-173">Para ver los detalles de una fábrica, haga clic en la fila de la lista de fábricas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="99c2d-174">Para ver los detalles de una línea de producción, haga clic en la fila de la lista.</span><span class="sxs-lookup"><span data-stu-id="99c2d-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="99c2d-175">Para ver los nodos OPC UA publicados de una estación de la línea de producción, haga clic en la fila en la lista.</span><span class="sxs-lookup"><span data-stu-id="99c2d-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="99c2d-176">Para ver los detalles en un nodo específico de la estación, haga clic en la fila en la lista.</span><span class="sxs-lookup"><span data-stu-id="99c2d-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="99c2d-177">Esta acción inicia el panel de contexto con visualizaciones de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99c2d-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="99c2d-178">Haga clic en estos gráficos para realizar más análisis en el entorno del explorador de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99c2d-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="99c2d-179">Visualización de mapas</span><span class="sxs-lookup"><span data-stu-id="99c2d-179">View map</span></span>

<span data-ttu-id="99c2d-180">Si su suscripción tiene acceso a la API de Bing Maps, el mapa *Fábricas* muestra la ubicación geográfica y el estado de todas las fábricas incluidas en la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="99c2d-181">Haga clic en las ubicaciones que se muestran en el mapa para profundizar en los detalles de ubicación.</span><span class="sxs-lookup"><span data-stu-id="99c2d-181">To drill into the location details, click the locations displayed on the map.</span></span>

![Mapa de la solución preconfigurada de fábrica conectada][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="99c2d-183">Visualización de alertas</span><span class="sxs-lookup"><span data-stu-id="99c2d-183">View alerts</span></span>

<span data-ttu-id="99c2d-184">El panel **Alerta** muestra las alertas generadas debido a que un valor notificado o un valor calculado de OEE o KPI supera el umbral configurado.</span><span class="sxs-lookup"><span data-stu-id="99c2d-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="99c2d-185">Este panel muestra las alertas en cada nivel de la jerarquía, desde la vista de nivel de estación a la vista global.</span><span class="sxs-lookup"><span data-stu-id="99c2d-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="99c2d-186">Las alertas contienen una descripción de la alerta, fecha, hora, ubicación y número de repeticiones.</span><span class="sxs-lookup"><span data-stu-id="99c2d-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="99c2d-187">Puede obtener más información de los datos que provocaron la alerta usando los datos de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99c2d-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="99c2d-188">Los datos de Time Series Insights se visualizan en las alertas, si procede.</span><span class="sxs-lookup"><span data-stu-id="99c2d-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="99c2d-189">Si es un administrador, puede realizar acciones predeterminadas en las alertas, tales como:</span><span class="sxs-lookup"><span data-stu-id="99c2d-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="99c2d-190">Cierre la alerta.</span><span class="sxs-lookup"><span data-stu-id="99c2d-190">Close the alert.</span></span>
* <span data-ttu-id="99c2d-191">Confirme la alerta.</span><span class="sxs-lookup"><span data-stu-id="99c2d-191">Acknowledge the alert.</span></span>

<span data-ttu-id="99c2d-192">Si lo desea, puede realizar acciones más complejas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="99c2d-193">Por ejemplo, para el nodo Presión de OPC UA del ensamblado, podría:</span><span class="sxs-lookup"><span data-stu-id="99c2d-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="99c2d-194">Mostrar información de soporte técnico en una página web de una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="99c2d-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="99c2d-195">Llamar a un método de OPC UA en el dispositivo que mitigue la causa de la alerta.</span><span class="sxs-lookup"><span data-stu-id="99c2d-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="99c2d-196">Suprimir la disponibilidad de las acciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-196">Suppress the availability of the default actions.</span></span>

    ![Alertas de la solución preconfigurada de fábrica conectada][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="99c2d-198">Estas alertas las generan las reglas que se especifican en un archivo de configuración de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="99c2d-199">Estas reglas pueden generar alertas cuando las cifras de OEE o KPI o los valores de nodo OPC UA superan el umbral configurado.</span><span class="sxs-lookup"><span data-stu-id="99c2d-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="99c2d-200">El **Panel de alertas** muestra las alertas generadas en esta solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="99c2d-201">Para ver los detalles de una alerta, haga clic en la alerta en el panel de alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="99c2d-202">Para analizar con mayor profundidad los datos de alerta, haga clic en el gráfico en el panel de alertas para abrir el entorno del explorador de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99c2d-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="99c2d-203">Para resolver la alerta, hay disponibles varias acciones en el panel de alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="99c2d-204">Elija la opción adecuada y haga clic en el botón del comando para ejecutar la acción.</span><span class="sxs-lookup"><span data-stu-id="99c2d-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="99c2d-205">Ver la eficiencia general de equipos</span><span class="sxs-lookup"><span data-stu-id="99c2d-205">View overall equipment efficiency</span></span>

<span data-ttu-id="99c2d-206">OEE evalúa la eficiencia del proceso de fabricación usando parámetros de operaciones clave relacionadas con la producción.</span><span class="sxs-lookup"><span data-stu-id="99c2d-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="99c2d-207">OEE es una medida estándar de la industria que se calcula multiplicando la tasa de disponibilidad, la tasa de rendimiento y la tasa de calidad: OEE = disponibilidad x rendimiento x calidad.</span><span class="sxs-lookup"><span data-stu-id="99c2d-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE de la solución preconfigurada de fábrica conectada][cf-img-oee]

1. <span data-ttu-id="99c2d-209">Para ver el valor de OEE en cualquier nivel de la jerarquía, vaya a la vista específica que necesite.</span><span class="sxs-lookup"><span data-stu-id="99c2d-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="99c2d-210">En esa vista, el valor de OEE se muestra en el panel junto con cada uno de los elementos que componen el porcentaje de OEE.</span><span class="sxs-lookup"><span data-stu-id="99c2d-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="99c2d-211">Para analizar con mayor profundidad el valor de OEE de cualquier nivel de los datos de la jerarquía, haga clic en los porcentajes de OEE, de disponibilidad, de rendimiento o de calidad.</span><span class="sxs-lookup"><span data-stu-id="99c2d-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="99c2d-212">Aparece un panel de contexto con visualizaciones proporcionadas por Time Series Insights que muestra datos de la última hora, las últimas 24 horas y los últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="99c2d-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualización TSI de la solución preconfigurada de fábrica conectada][cf-img-tsi-visualization]

3. <span data-ttu-id="99c2d-214">Para analizar con mayor profundidad los datos de las alertas, haga clic en el gráfico en el panel de alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="99c2d-215">Esta acción abre el entorno de explorador de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="99c2d-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![Explorador de TSI de la solución preconfigurada de fábrica conectada][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="99c2d-217">Visualización de los indicadores clave de rendimiento</span><span class="sxs-lookup"><span data-stu-id="99c2d-217">View Key Performance Indicators</span></span>

<span data-ttu-id="99c2d-218">La solución proporciona dos indicadores clave de rendimiento, *unidades por hora* y *energía utilizada en kWh*.</span><span class="sxs-lookup"><span data-stu-id="99c2d-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI de la solución preconfigurada de fábrica conectada][cf-img-kpi]

1. <span data-ttu-id="99c2d-220">Para ver las unidades por hora o la energía usada de cualquier nivel de la jerarquía, vaya a la vista específica que necesite.</span><span class="sxs-lookup"><span data-stu-id="99c2d-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="99c2d-221">Las unidades por hora y la energía usada se muestran en el panel.</span><span class="sxs-lookup"><span data-stu-id="99c2d-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="99c2d-222">Para analizar las unidades por hora o la energía usada en cualquier nivel de la jerarquía, haga clic en el medidor del panel **Indicadores clave de rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="99c2d-223">Aparece un panel de contexto con las visualizaciones proporcionadas por Time Series Insights que permite ver los datos de la última hora, las últimas 24 horas y los últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="99c2d-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="99c2d-224">Revisión del escenario</span><span class="sxs-lookup"><span data-stu-id="99c2d-224">Scenario review</span></span>

<span data-ttu-id="99c2d-225">En este escenario, ha supervisado los valores de OEE y KPI de las fábricas en el panel.</span><span class="sxs-lookup"><span data-stu-id="99c2d-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="99c2d-226">A continuación, ha utilizado Time Series Insights para proporcionar más información para ayudar a profundizar en los datos de telemetría de OEE y KPI, y ayudar a detectar anomalías.</span><span class="sxs-lookup"><span data-stu-id="99c2d-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="99c2d-227">También ha utilizado el panel de alertas para visualizar los problemas en las fábricas y ha utilizado las acciones disponibles para resolver la alerta.</span><span class="sxs-lookup"><span data-stu-id="99c2d-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="99c2d-228">Otras características</span><span class="sxs-lookup"><span data-stu-id="99c2d-228">Other features</span></span>

<span data-ttu-id="99c2d-229">Las secciones siguientes describen algunas características adicionales de la solución de fábrica conectada que no se han descrito en el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="99c2d-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="99c2d-230">Aplicación de filtros</span><span class="sxs-lookup"><span data-stu-id="99c2d-230">Apply filters</span></span>

1. <span data-ttu-id="99c2d-231">Haga clic en las **comillas angulares** para mostrar una lista de los filtros disponibles en el panel de ubicaciones de fábrica o en el panel de alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="99c2d-232">Se muestra el panel de filtros.</span><span class="sxs-lookup"><span data-stu-id="99c2d-232">The filters panel is displayed for you.</span></span> 

    ![Filtros de la solución preconfigurada de fábrica conectada][cf-img-alert-filter]

3. <span data-ttu-id="99c2d-234">Elija el filtro que necesite.</span><span class="sxs-lookup"><span data-stu-id="99c2d-234">Choose the filter that you require.</span></span> <span data-ttu-id="99c2d-235">También puede escribir texto libre en los campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="99c2d-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="99c2d-236">A continuación, se aplica el filtro.</span><span class="sxs-lookup"><span data-stu-id="99c2d-236">The filter is then applied for you.</span></span> <span data-ttu-id="99c2d-237">El estado del filtro se muestra en el panel mediante un embudo que se muestra en las tablas de fábricas y alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![Filtros de la solución preconfigurada de fábrica conectada][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="99c2d-239">Un filtro activo no afecta a los valores de OEE y KPI mostrados, solo se filtra el contenido de la lista.</span><span class="sxs-lookup"><span data-stu-id="99c2d-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="99c2d-240">Para borrar un filtro, haga clic en el embudo y haga clic en el filtro en el panel de contexto de filtro.</span><span class="sxs-lookup"><span data-stu-id="99c2d-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="99c2d-241">Se muestra el texto **Todos** en las tablas de fábricas y alertas.</span><span class="sxs-lookup"><span data-stu-id="99c2d-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="99c2d-242">Examinar un servidor de OPC UA</span><span class="sxs-lookup"><span data-stu-id="99c2d-242">Browse an OPC UA server</span></span>

<span data-ttu-id="99c2d-243">Al implementar la solución preconfigurada, se aprovisionan automáticamente los servidores de OPC UA simulados que se pueden examinar mediante el explorador de la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="99c2d-244">Estos servidores son *servidores de OPC UA simulados*.</span><span class="sxs-lookup"><span data-stu-id="99c2d-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="99c2d-245">Los servidores simulados facilitan la experimentación de la solución preconfigurada sin necesidad de implementar servidores físicos reales.</span><span class="sxs-lookup"><span data-stu-id="99c2d-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="99c2d-246">Si quiere conectar un servidor de OPC UA real a la solución, consulte cómo [conectar su dispositivo OPC UA a la solución preconfigurada de fábrica conectada][lnk-connect-cf].</span><span class="sxs-lookup"><span data-stu-id="99c2d-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="99c2d-247">Haga clic en el **icono de fábrica** en la barra de navegación del panel.</span><span class="sxs-lookup"><span data-stu-id="99c2d-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![Explorador de servidores de la solución preconfigurada de fábrica conectada][cf-img-server-browser]

2. <span data-ttu-id="99c2d-249">Elija uno de los servidores de la lista preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="99c2d-250">Esta lista muestra los servidores que se implementan en la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![Selección del servidor de la solución preconfigurada de fábrica conectada][cf-img-server-choice]

3. <span data-ttu-id="99c2d-252">Haga clic en **Conectar**; aparece un cuadro de diálogo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99c2d-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="99c2d-253">Para la simulación, es seguro hacer clic en **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="99c2d-254">Haga clic en cualquiera de los nodos del árbol de servidores para expandirlo.</span><span class="sxs-lookup"><span data-stu-id="99c2d-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="99c2d-255">Los nodos que publican telemetría tienen una marca de verificación junto a ellos.</span><span class="sxs-lookup"><span data-stu-id="99c2d-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Árbol de servidores de la solución preconfigurada de fábrica conectada][cf-img-server-tree]

5. <span data-ttu-id="99c2d-257">Haga clic con el botón derecho para leer, escribir, publicar o llamar a ese nodo.</span><span class="sxs-lookup"><span data-stu-id="99c2d-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="99c2d-258">Las acciones disponibles dependen de los permisos y los atributos del nodo.</span><span class="sxs-lookup"><span data-stu-id="99c2d-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="99c2d-259">La opción de lectura muestra un panel de contexto que muestra el valor de un nodo específico.</span><span class="sxs-lookup"><span data-stu-id="99c2d-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="99c2d-260">La opción de escritura muestra un panel de contexto donde puede escribir un nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="99c2d-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="99c2d-261">La opción de llamada muestra un nodo donde puede especificar los parámetros para la llamada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="99c2d-262">Publicación de un nodo</span><span class="sxs-lookup"><span data-stu-id="99c2d-262">Publish a node</span></span>

<span data-ttu-id="99c2d-263">Cuando se examina un *servidor de OPC UA simulado*, también puede elegir publicar nuevos nodos.</span><span class="sxs-lookup"><span data-stu-id="99c2d-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="99c2d-264">Puede analizar la telemetría de estos nodos en la solución.</span><span class="sxs-lookup"><span data-stu-id="99c2d-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="99c2d-265">Estos *servidores de OPC UA simulados* facilitan la experimentación de la solución preconfigurada sin necesidad de implementar dispositivos físicos reales.</span><span class="sxs-lookup"><span data-stu-id="99c2d-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="99c2d-266">Vaya a un nodo en el árbol del explorador de servidores de OPC UA que desea publicar.</span><span class="sxs-lookup"><span data-stu-id="99c2d-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="99c2d-267">Haga clic con el botón derecho en el nodo.</span><span class="sxs-lookup"><span data-stu-id="99c2d-267">Right-click the node.</span></span>

3. <span data-ttu-id="99c2d-268">Elija **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-268">Choose **Publish**.</span></span>

    ![Nodo de publicación de fábrica conectada][cf-img-publish-node]

4. <span data-ttu-id="99c2d-270">Aparece un panel de contexto que le indica que la publicación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="99c2d-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="99c2d-271">El nodo aparece en la vista de nivel de estación con una marca de verificación junto a él.</span><span class="sxs-lookup"><span data-stu-id="99c2d-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![Publicación correcta en la solución preconfigurada de fábrica conectada][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="99c2d-273">Comando y control</span><span class="sxs-lookup"><span data-stu-id="99c2d-273">Command and control</span></span>

<span data-ttu-id="99c2d-274">La fábrica conectada le permite enviar órdenes y controlar los dispositivos industriales directamente desde la nube.</span><span class="sxs-lookup"><span data-stu-id="99c2d-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="99c2d-275">Puede utilizar esta característica para responder a las alertas generadas por el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="99c2d-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="99c2d-276">Por ejemplo, podría enviar un comando al dispositivo desde la nube.</span><span class="sxs-lookup"><span data-stu-id="99c2d-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="99c2d-277">Puede encontrar los comandos disponibles en el nodo **StationCommands** del árbol del explorador de servidores de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="99c2d-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="99c2d-278">En este escenario, se abre una válvula de despresurización en la estación de ensamblado de una línea de producción en Munich.</span><span class="sxs-lookup"><span data-stu-id="99c2d-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="99c2d-279">Para usar la funcionalidad de comando y control, debe estar en el rol **Administrador** en la implementación de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="99c2d-280">Vaya al nodo **StationCommands** del árbol del explorador de servidores de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="99c2d-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="99c2d-281">Elija el comando que desea usar.</span><span class="sxs-lookup"><span data-stu-id="99c2d-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="99c2d-282">Haga clic con el botón derecho en el nodo.</span><span class="sxs-lookup"><span data-stu-id="99c2d-282">Right-click the node.</span></span>

4. <span data-ttu-id="99c2d-283">Elija **Llamada**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-283">Choose **Call**.</span></span>

    ![Comando de llamada de la solución preconfigurada de fábrica conectada][cf-img-call-command]

5. <span data-ttu-id="99c2d-285">Aparece un panel de contexto que le informa del método al que va a llamar, y, en su caso, los detalles de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="99c2d-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="99c2d-286">Elija **Llamada**.</span><span class="sxs-lookup"><span data-stu-id="99c2d-286">Choose **Call**.</span></span>

    ![Contexto de llamada de la solución preconfigurada de fábrica conectada][cf-img-call-context]

7. <span data-ttu-id="99c2d-288">El panel de contexto se actualiza para informarle de que la llamada al método se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="99c2d-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="99c2d-289">Para comprobar que la llamada se realizó correctamente, lea el valor del nodo de presión que se ha actualizado como resultado de la llamada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![Llamada correcta de la solución preconfigurada de fábrica conectada][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="99c2d-291">Entre bambalinas</span><span class="sxs-lookup"><span data-stu-id="99c2d-291">Behind the scenes</span></span>

<span data-ttu-id="99c2d-292">Al implementar una solución preconfigurada, el proceso de implementación crea varios recursos en la suscripción de Azure seleccionada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="99c2d-293">Dichos recursos se pueden ver en Azure [Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="99c2d-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="99c2d-294">El proceso de implementación crea un **grupo de recursos** cuyo nombre se basa en el nombre que eligió para la solución preconfigurada:</span><span class="sxs-lookup"><span data-stu-id="99c2d-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Solución preconfigurada en el portal de Azure][img-cf-portal]

<span data-ttu-id="99c2d-296">Para ver la configuración de cada recurso, selecciónelo en la lista de recursos del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99c2d-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="99c2d-297">También puede ver el código fuente de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="99c2d-298">El código fuente de la solución preconfigurada de fábrica conectada está en el repositorio de GitHub [azure-iot-connected-factory][lnk-cfgithub]:</span><span class="sxs-lookup"><span data-stu-id="99c2d-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="99c2d-299">Cuando haya terminado, puede eliminar la solución preconfigurada de la suscripción de Azure en el sitio [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="99c2d-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="99c2d-300">Este sitio le permite eliminar fácilmente todos los recursos que se aprovisionaron cuando creó la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="99c2d-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="99c2d-301">Para asegurarse de eliminar todo lo relacionado con la solución preconfigurada, elimínelo en el sitio [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="99c2d-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="99c2d-302">No elimine el grupo de recursos en el portal.</span><span class="sxs-lookup"><span data-stu-id="99c2d-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99c2d-303">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99c2d-303">Next Steps</span></span>

<span data-ttu-id="99c2d-304">Ahora que ha implementado una solución preconfigurada de trabajo, puede continuar su introducción al Conjunto de aplicaciones de IoT con la lectura de los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="99c2d-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="99c2d-305">[Tutorial de la solución preconfigurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="99c2d-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="99c2d-306">[Conexión del dispositivo a la solución preconfigurada de fábrica conectada][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="99c2d-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="99c2d-307">[Permisos en el sitio azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="99c2d-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md