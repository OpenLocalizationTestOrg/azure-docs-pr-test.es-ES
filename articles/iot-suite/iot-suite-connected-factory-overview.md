---
title: "aaaAzure IoT Suite conectado información general sobre generador | Documentos de Microsoft"
description: "Una descripción de hello Azure IoT Suite conectado solución preconfigurada de fábrica."
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="4f2e3-103">Empezar a trabajar con soluciones de fábrica preconfigurado Hola conectado</span><span class="sxs-lookup"><span data-stu-id="4f2e3-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="4f2e3-104">Conjunto de Azure IoT [soluciones preconfiguradas] [ lnk-preconfigured-solutions] combinar varias IoT de Azure servicios toodeliver-to-end soluciones que implementan escenarios empresariales IoT.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="4f2e3-105">Hola *generador conectado* solución preconfigurada conecta tooand supervisa los dispositivos industriales.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="4f2e3-106">Puede usar Hola solución tooanalyze Hola flujo de datos de los dispositivos y la productividad operativa toodrive y la rentabilidad.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="4f2e3-107">Este tutorial muestra cómo tooprovision Hola conectado fábrica preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="4f2e3-108">También le guía a través de características básicas de Hola de solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="4f2e3-109">Puede tener acceso a muchas de estas características de solución de hello *panel* que implementa como parte de la solución de hello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![panel de la solución preconfigurada de fábrica conectada][img-cf-home]

<span data-ttu-id="4f2e3-111">toocomplete este tutorial, necesita una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4f2e3-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4f2e3-113">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="4f2e3-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="4f2e3-114">Solución de Hola de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="4f2e3-114">Provision hello solution</span></span>

1. <span data-ttu-id="4f2e3-115">Inicie sesión con sus credenciales de cuenta de Azure de tooazureiotsuite.com y haga clic en "**+**" toocreate una solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="4f2e3-116">Haga clic en **seleccione** en hello **generador conectado** icono.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="4f2e3-117">Escriba un valor en **Nombre de la solución** para la solución preconfigurada de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="4f2e3-118">Seleccione hello **suscripción** y **región** desea toouse tooprovision Hola solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="4f2e3-119">Haga clic en **crear solución** hello toobegin proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="4f2e3-120">Este proceso suele tarda varios toorun minutos.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="4f2e3-121">Mientras esperan hello toocomplete del proceso de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="4f2e3-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="4f2e3-122">Haga clic en el icono de hello para la solución con **Provisioning** estado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="4f2e3-123">Hola aviso **aprovisionamiento estados** tal y como se implementan los servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="4f2e3-124">Una vez que finalice el aprovisionamiento, Hola cambios de estado demasiado**listo**.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="4f2e3-125">Haga clic en detalles del hello toosee Hola icono de la solución en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="4f2e3-126">Si encuentra problemas al implementar soluciones de hello preconfigurado, consulte [permisos en el sitio de hello azureiotsuite.com] [ lnk-permissions] hello y [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="4f2e3-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="4f2e3-127">Si continúan los problemas de hello, crear un vale de servicio en hello [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="4f2e3-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="4f2e3-128">¿Hay detalles que se esperaría toosee que no aparezcan para su solución?</span><span class="sxs-lookup"><span data-stu-id="4f2e3-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="4f2e3-129">Puede sugerirnos nuevas características en [User Voice](https://feedback.azure.com/forums/321918-azure-iot)(La voz del usuario).</span><span class="sxs-lookup"><span data-stu-id="4f2e3-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="4f2e3-130">Información general de escenario</span><span class="sxs-lookup"><span data-stu-id="4f2e3-130">Scenario overview</span></span>

<span data-ttu-id="4f2e3-131">Al implementar Hola conectado fábrica preconfigurado solución, se rellena previamente con recursos que le permiten toostep a través de un escenario industrial común.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="4f2e3-132">En este escenario, varias fábricas conectan informes de solución de toohello toocompute requiere valores de los datos de Hola la eficacia general de equipos (OEE) y los indicadores clave de rendimiento (KPI).</span><span class="sxs-lookup"><span data-stu-id="4f2e3-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="4f2e3-133">Hello las secciones siguientes muestran cómo para:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="4f2e3-134">Supervisar los valores de la fábrica, las líneas de producción, el valor de OEE de las estaciones y los valores de KPI</span><span class="sxs-lookup"><span data-stu-id="4f2e3-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="4f2e3-135">Analizar los datos de telemetría de hello generados a partir de estos dispositivos con visión de serie de tiempo de Azure</span><span class="sxs-lookup"><span data-stu-id="4f2e3-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="4f2e3-136">Actuar sobre los problemas de toofix de alertas</span><span class="sxs-lookup"><span data-stu-id="4f2e3-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="4f2e3-137">Una característica clave de este escenario es que puede realizar todas estas acciones de forma remota desde el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="4f2e3-138">No es necesario dispositivos toohello de acceso físico.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="4f2e3-139">Panel de vista Hola solución</span><span class="sxs-lookup"><span data-stu-id="4f2e3-139">View hello solution dashboard</span></span>

<span data-ttu-id="4f2e3-140">panel de la solución de Hello permite toomanage solución de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="4f2e3-141">Es una representación jerárquica de una configuración de fábrica global.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="4f2e3-142">Por ejemplo, puede ver los valores de OEE y KPI, publicar nuevos nodos para telemetría y actuar sobre las alertas.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="4f2e3-143">Cuando el aprovisionamiento de hello está completado e indica el icono de Hola para su solución preconfigurada **listo**, elija **iniciar** tooopen el portal de solución de fábrica conectados en una nueva pestaña.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Iniciar solución de hello preconfigurado][img-launch-solution]

1. <span data-ttu-id="4f2e3-145">De forma predeterminada, el portal de solución de hello muestra hello *panel*.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="4f2e3-146">toonavigate tooother áreas del portal de hello, use menú de hello en el lado izquierdo de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Panel de la solución preconfigurada de fábrica conectada][cf-img-menu]

<span data-ttu-id="4f2e3-148">panel de Hello muestra hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="4f2e3-149">A **lista generador** panel que muestra el estado de hello, la ubicación y la configuración de producción actual de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="4f2e3-150">Cuando ejecuta por primera vez solución hello, hay un número de dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="4f2e3-151">simulación de la línea de producción de Hello se compone de tres real OPC UA servidores por línea de producción que realicen tareas simuladas y compartan datos.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="4f2e3-152">Para obtener más información sobre OPC UA, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="4f2e3-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="4f2e3-153">A **mapa** que muestra hello ubicación de cada dispositivo conectado toohello solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="4f2e3-154">solución de Hello puede utilizar información de tooplot de API de Bing Maps de hello en el mapa de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="4f2e3-155">Si la suscripción está habilitada para la API de Bing Maps Enterprise, esta característica se usa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="4f2e3-156">Si no es así, consulte hello [preguntas más frecuentes sobre] [ lnk-faq] toolearn cómo toomake Hola dinámicos de mapa.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="4f2e3-157">Un panel de **Alertas**, que muestra las alertas generadas cuando un valor de OEE, KPI o telemetría supera un umbral específico.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="4f2e3-158">Un **la eficacia general de equipos** panel que muestra valores de hello OEE para toda la empresa Hola o generador de Hola o de producción de línea/estación está viendo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="4f2e3-159">Este valor se agrega desde el nivel de empresa de hello estación vista toohello.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="4f2e3-160">ilustración de Hello OEE y sus elementos constituyentes se pueden analizar aún más.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="4f2e3-161">**Indicadores clave de rendimiento** panel que muestra hello número de unidades producidas y energía usada por toda la empresa Hola o línea de fábrica o de producción de hello/estación está viendo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="4f2e3-162">Estos valores se agregan desde un nivel de empresa de estación vista toohello.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="4f2e3-163">Visualización de fábricas</span><span class="sxs-lookup"><span data-stu-id="4f2e3-163">View factories</span></span>

<span data-ttu-id="4f2e3-164">Hola *generadores* Hola ubicación geográfica de todos los generadores de hello en soluciones de hello, su estado y la configuración de producción actual se muestra en el panel.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="4f2e3-165">Desde la lista de ubicaciones de hello, puede navegar toohello otros niveles de jerarquía de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="4f2e3-166">Hola lista Hola son hipervínculos que se vinculan los detalles de las líneas de producción de hello en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="4f2e3-167">A continuación, es posible toodrill en los detalles de la línea de producción de hello y hacia abajo de la vista de nivel de estación de toohello.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="4f2e3-168">También puede aplicar una lista de toohello de filtros.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-168">You can also apply a filter toohello list.</span></span>

![Fábricas de la solución preconfigurada de fábrica conectada][cf-img-factories] 

1. <span data-ttu-id="4f2e3-170">Hola **panel Generador** muestra Hola lista de fábrica para esta solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="4f2e3-171">lista de fábrica de Hello inicialmente muestra seis generadores creados por el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="4f2e3-172">Puede agregar más dispositivos simulados y físicos toohello solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="4f2e3-173">detalles de hello tooview de un generador, haga clic en la fila de hello en la lista de fábrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="4f2e3-174">detalles de hello tooview de una línea de producción, haga clic en la fila de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="4f2e3-175">tooview Hola publica nodos OPC UA de una estación en la línea de producción de hello, haga clic en lista de Hola de fila de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="4f2e3-176">detalles de tooview en un nodo específico en la estación de hello, haga clic en la fila de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="4f2e3-177">Esta acción inicia el panel de contexto Hola con visualizaciones de visión de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="4f2e3-178">Haga clic en estos gráficos toodo un análisis más profundo en entorno de explorador de hello visión de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="4f2e3-179">Visualización de mapas</span><span class="sxs-lookup"><span data-stu-id="4f2e3-179">View map</span></span>

<span data-ttu-id="4f2e3-180">Si su suscripción tiene acceso toohello API de Bing Maps, Hola *generadores* mapa muestra ubicación geográfica de Hola y el estado de todos los generadores de hello en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="4f2e3-181">toodrill en los detalles de la ubicación de hello, haga clic en ubicaciones de Hola que se muestra en el mapa de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Mapa de la solución preconfigurada de fábrica conectada][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="4f2e3-183">Visualización de alertas</span><span class="sxs-lookup"><span data-stu-id="4f2e3-183">View alerts</span></span>

<span data-ttu-id="4f2e3-184">Hola **alerta** panel muestra las alertas generadas debido tooa notifica el valor o un valor calculado de OEE o KPI que supera el umbral configurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="4f2e3-185">Este panel muestra las alertas en cada nivel de jerarquía de hello, desde Hola estación nivel toohello global ver.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="4f2e3-186">alertas de Hello contienen una descripción de alerta de hello, fecha, hora, ubicación y número de repeticiones.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="4f2e3-187">Puede obtener información en datos toohello que provocó la alerta hello mediante Hola información de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="4f2e3-188">Hola tiempo serie visión datos se visualizarán en Hola alertas si procede.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="4f2e3-189">Si es administrador, puede realizar acciones predeterminadas en las alertas de hello como:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="4f2e3-190">Alerta de cierre Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-190">Close hello alert.</span></span>
* <span data-ttu-id="4f2e3-191">Confirmar la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="4f2e3-192">Si lo desea, puede realizar acciones más complejas.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="4f2e3-193">Por ejemplo, para hello nodo de agente de usuario de OPC presión de hello ensamblado se puede realizar:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="4f2e3-194">Mostrar información de soporte técnico en una página web de una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="4f2e3-195">Mitigue la causa de Hola de alerta de hello mediante una llamada a un método de OPC UA en dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="4f2e3-196">Suprimir disponibilidad Hola de acciones predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-196">Suppress hello availability of hello default actions.</span></span>

    ![Alertas de la solución preconfigurada de fábrica conectada][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="4f2e3-198">Estas alertas se generan las reglas que se especifican en un archivo de configuración de solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="4f2e3-199">Estas reglas pueden generar alertas cuando Hola OEE o cifras KPI o valores de los nodos de agente de usuario de OPC supera el umbral configurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="4f2e3-200">Hola **panel alertas** muestra Hola alertas generadas en esta solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="4f2e3-201">detalles de hello tooview de una alerta, haga clic en la alerta de hello en el panel de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="4f2e3-202">toofurther analizar datos de alertas de hello, haga clic en gráfico de hello en entorno de explorador de hello panel alerta tooopen Hola visión de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="4f2e3-203">tooaddress Hola alerta, varias acciones están disponibles en el panel alertas Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="4f2e3-204">Elija Hola la opción adecuada para usted y haga clic en hello ejecutar botón de comando de acción.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="4f2e3-205">Ver la eficiencia general de equipos</span><span class="sxs-lookup"><span data-stu-id="4f2e3-205">View overall equipment efficiency</span></span>

<span data-ttu-id="4f2e3-206">Las tasas OEE Hola eficacia del proceso de fabricación de hello mediante una clave parámetros operativos relacionadas con la producción.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="4f2e3-207">OEE es una medida estándar se calcula multiplicando la velocidad de disponibilidad de hello, la velocidad de rendimiento y velocidad de calidad de la industria: OEE = disponibilidad x calidad del rendimiento x.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE de la solución preconfigurada de fábrica conectada][cf-img-oee]

1. <span data-ttu-id="4f2e3-209">tooview OEE en cualquier nivel de jerarquía de hello, navegue toohello vista específica que necesite.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="4f2e3-210">Hola OEE para esa vista muestra en el panel de hello junto con cada uno de los elementos de Hola que componen el porcentaje OEE Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="4f2e3-211">toofurther analizar hello OEE para cualquier nivel de datos de la jerarquía de hello, haga clic en hello OEE, disponibilidad, rendimiento o porcentaje de calidad.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="4f2e3-212">Aparece un panel de contexto con información de la serie de tiempo alimentados visualizaciones que muestran datos de hello última hora, últimas 24 horas y últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualización TSI de la solución preconfigurada de fábrica conectada][cf-img-tsi-visualization]

3. <span data-ttu-id="4f2e3-214">toofurther analizar datos de alertas de hello, haga clic en gráfico de hello en el panel alertas Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="4f2e3-215">Esta acción abre el entorno de explorador de hello visión de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Explorador de TSI de la solución preconfigurada de fábrica conectada][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="4f2e3-217">Visualización de los indicadores clave de rendimiento</span><span class="sxs-lookup"><span data-stu-id="4f2e3-217">View Key Performance Indicators</span></span>

<span data-ttu-id="4f2e3-218">solución de Hello proporciona dos indicadores clave de rendimiento, *unidades por hora* y *energía utilizada en kWh*.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI de la solución preconfigurada de fábrica conectada][cf-img-kpi]

1. <span data-ttu-id="4f2e3-220">unidades de tooview por hora o de energía utilizada en cualquier nivel de jerarquía de hello, navegue toohello vista específica que necesite.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="4f2e3-221">las unidades de Hola por hora y energía usan mostrar en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="4f2e3-222">unidades de tooanalyze por hora o de energía utilizada en cualquier nivel de jerarquía de hello aún más, haga clic en medidor Hola Hola **indicadores clave de rendimiento** panel.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="4f2e3-223">Aparece un panel de contexto con visualizaciones de visión de la serie de tiempo con la tecnología de lo que los datos de tooview de hello última hora, Hola últimas 24 horas y los últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="4f2e3-224">Revisión del escenario</span><span class="sxs-lookup"><span data-stu-id="4f2e3-224">Scenario review</span></span>

<span data-ttu-id="4f2e3-225">En este escenario, está supervisando los valores OEE y KPI de generadores, en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="4f2e3-226">A continuación, usó tooprovide visión de la serie de tiempo más información toohelp profundizar aún más los datos de telemetría de Hola para toohelp OEE y KPI con detección de anomalías.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="4f2e3-227">También usa tooview problemas de hello panel alerta con los generadores y usa alerta de hello acciones disponibles tooyou tooresolve Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="4f2e3-228">Otras características</span><span class="sxs-lookup"><span data-stu-id="4f2e3-228">Other features</span></span>

<span data-ttu-id="4f2e3-229">Hola siguientes secciones describe algunas características adicionales de solución de fábrica de hello conectado que no se describen en el escenario anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="4f2e3-230">Aplicación de filtros</span><span class="sxs-lookup"><span data-stu-id="4f2e3-230">Apply filters</span></span>

1. <span data-ttu-id="4f2e3-231">Haga clic en hello **comillas angulares** toodisplay una lista de filtros disponibles en el panel de ubicaciones de fábrica de Hola o panel de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="4f2e3-232">se muestra el panel de filtros de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-232">hello filters panel is displayed for you.</span></span> 

    ![Filtros de la solución preconfigurada de fábrica conectada][cf-img-alert-filter]

3. <span data-ttu-id="4f2e3-234">Seleccione el filtro de Hola que necesite.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-234">Choose hello filter that you require.</span></span> <span data-ttu-id="4f2e3-235">También es posible tootype texto libre en los campos de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="4f2e3-236">a continuación, se aplica el filtro de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-236">hello filter is then applied for you.</span></span> <span data-ttu-id="4f2e3-237">También se muestra el estado del filtro Hello en panel de Hola a través de un embudo que muestra de generadores de Hola y tablas de alertas.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Filtros de la solución preconfigurada de fábrica conectada][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="4f2e3-239">Un filtro activo no afecta a hello muestra valores OEE y KPI, solo filtra mostrar el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="4f2e3-240">tooclear un filtro, haga clic en el embudo de Hola y haga clic en filtro en el panel de contexto de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="4f2e3-241">Hola texto **todos los** se muestra en los generadores de Hola y tablas de alertas.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="4f2e3-242">Examinar un servidor de OPC UA</span><span class="sxs-lookup"><span data-stu-id="4f2e3-242">Browse an OPC UA server</span></span>

<span data-ttu-id="4f2e3-243">Al implementar soluciones de hello preconfigurado, aprovisionar automáticamente los servidores de OPC UA simulados que se pueden examinar mediante el Explorador de soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="4f2e3-244">Estos servidores son *servidores de OPC UA simulados*.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="4f2e3-245">Servidores simulados facilitan automáticamente tooexperiment con la solución de hello preconfigurado sin Hola necesidad toodeploy real, físico los servidores.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="4f2e3-246">Si desea tooconnect una solución de toohello de servidor de OPC UA real, vea hello [conectarse a la solución de fábrica preconfigurado de OPC UA dispositivo toohello conectado] [ lnk-connect-cf] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="4f2e3-247">Haga clic en hello **icono generador** en la barra de navegación del panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Explorador de servidores de la solución preconfigurada de fábrica conectada][cf-img-server-browser]

2. <span data-ttu-id="4f2e3-249">Elija uno de los servidores de Hola de lista preconfigurada Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="4f2e3-250">Esta lista muestra los servidores de Hola que se implementan en soluciones de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Selección del servidor de la solución preconfigurada de fábrica conectada][cf-img-server-choice]

3. <span data-ttu-id="4f2e3-252">Haga clic en **Conectar**; aparece un cuadro de diálogo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="4f2e3-253">Simulación de hello, resulta seguro tooclick **continuar**</span><span class="sxs-lookup"><span data-stu-id="4f2e3-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="4f2e3-254">tooexpand cualquiera de los nodos de hello en el árbol de servidores de hello, haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="4f2e3-255">Los nodos que publican telemetría tienen una marca de verificación junto a ellos.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Árbol de servidores de la solución preconfigurada de fábrica conectada][cf-img-server-tree]

5. <span data-ttu-id="4f2e3-257">Haga clic en un elemento tooread, escribir, publicar o llame a ese nodo.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="4f2e3-258">tooyou de Hello las acciones disponibles dependen de los permisos y atributos de hello del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="4f2e3-259">Hola lee opción toodisplays un panel de contexto Mostrar valor de Hola de nodo específico Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="4f2e3-260">Hola escribir opción muestra un panel de contexto donde puede escribir un nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="4f2e3-261">opción de llamada de Hello muestra un nodo donde puede especificar parámetros de Hola para llamada Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="4f2e3-262">Publicación de un nodo</span><span class="sxs-lookup"><span data-stu-id="4f2e3-262">Publish a node</span></span>

<span data-ttu-id="4f2e3-263">Cuando se examina un *servidor simulado de OPC UA*, también puede elegir toopublish nuevos nodos.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="4f2e3-264">Puede analizar la telemetría de Hola de estos nodos de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="4f2e3-265">Estos *simulados servidores OPC UA* que sea fácil tooexperiment con soluciones de hello preconfigurado sin implementar dispositivos físicos reales.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="4f2e3-266">Buscar nodo tooa en el árbol del explorador de servidores de OPC UA que desea toopublish Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="4f2e3-267">Haga clic en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-267">Right-click hello node.</span></span>

3. <span data-ttu-id="4f2e3-268">Elija **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-268">Choose **Publish**.</span></span>

    ![Nodo de publicación de fábrica conectada][cf-img-publish-node]

4. <span data-ttu-id="4f2e3-270">Un panel de contexto aparece lo que indica que Hola de publicación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="4f2e3-271">nodo de Hello aparece en la vista de nivel de estación de hello con una marca de verificación junto a él.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Publicación correcta en la solución preconfigurada de fábrica conectada][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="4f2e3-273">Comando y control</span><span class="sxs-lookup"><span data-stu-id="4f2e3-273">Command and control</span></span>

<span data-ttu-id="4f2e3-274">Hola conectado generador permite comandos y controlar los dispositivos de la industria directamente desde la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="4f2e3-275">Puede usar este tooalerts de toorespond característica generados por dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="4f2e3-276">Por ejemplo, podría enviar un dispositivo de toohello de comando de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="4f2e3-277">Puede encontrar Hola comandos disponibles en hello **StationCommands** nodo de árbol del explorador de servidores de OPC UA Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="4f2e3-278">En este escenario, se abrirá una válvula de versión en la estación de ensamblado hello de una línea de producción de Munich.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="4f2e3-279">funcionalidad de comando y control de hello toouse, debe estar en hello **administrador** rol para hello preconfigurado implementación de la solución.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="4f2e3-280">Examinar toohello **StationCommands** nodo de árbol del explorador de servidores de OPC UA Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="4f2e3-281">Elija el comando de Hola que desea usar.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="4f2e3-282">Haga clic en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-282">Right-click hello node.</span></span>

4. <span data-ttu-id="4f2e3-283">Elija **Llamada**.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-283">Choose **Call**.</span></span>

    ![Comando de llamada de la solución preconfigurada de fábrica conectada][cf-img-call-command]

5. <span data-ttu-id="4f2e3-285">Aparece de un panel de contexto que le informa de qué método va toocall y los detalles de los parámetros es aplicable.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="4f2e3-286">Elija **Llamada**.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-286">Choose **Call**.</span></span>

    ![Contexto de llamada de la solución preconfigurada de fábrica conectada][cf-img-call-context]

7. <span data-ttu-id="4f2e3-288">panel de contexto de Hello es tooinform actualizado que Hola llamada al método se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="4f2e3-289">Puede comprobar llamada Hola leyendo Hola valor del nodo de presión de Hola que actualizado como resultado de llamada de Hola se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Llamada correcta de la solución preconfigurada de fábrica conectada][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="4f2e3-291">Entre bastidores de Hola</span><span class="sxs-lookup"><span data-stu-id="4f2e3-291">Behind hello scenes</span></span>

<span data-ttu-id="4f2e3-292">Al implementar una solución preconfigurada, el proceso de implementación de hello crea varios recursos en hello Azure suscripción que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="4f2e3-293">Puede ver estos recursos en hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="4f2e3-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="4f2e3-294">proceso de implementación de Hello crea un **grupo de recursos** con un nombre basado en el nombre de Hola que elija para su solución preconfigurada:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Solución preconfigurada en hello portal de Azure][img-cf-portal]

<span data-ttu-id="4f2e3-296">Puede ver configuración de Hola de cada recurso mediante su selección en la lista de Hola de recursos de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="4f2e3-297">También puede ver el código fuente de hello para la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="4f2e3-298">Hello conectado fábrica preconfigurado solución código fuente está en hello [-iot-conectado-factory de azure] [ lnk-cfgithub] repositorio de GitHub:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="4f2e3-299">Cuando haya terminado, puede eliminar solución Hola preconfigurado de su suscripción de Azure en hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="4f2e3-300">Este sitio le permite eliminar tooeasily que todos Hola recursos que estaban aprovisionados al crear soluciones de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4f2e3-301">tooensure eliminar todos los elementos relacionados con la solución toohello preconfigurado, eliminarlo de hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="4f2e3-302">No se elimine el grupo de recursos de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f2e3-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f2e3-303">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f2e3-303">Next Steps</span></span>

<span data-ttu-id="4f2e3-304">Ahora que ha implementado una solución de trabajo configurado preconfigurada, puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="4f2e3-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="4f2e3-305">[Tutorial de la solución preconfigurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="4f2e3-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="4f2e3-306">[Conectarse a la solución de fábrica conectado preconfigurado toohello de dispositivo][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="4f2e3-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="4f2e3-307">[Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="4f2e3-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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