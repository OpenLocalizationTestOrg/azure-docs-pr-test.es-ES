---
title: "Solución preconfigurada de mantenimiento predictivo |Microsoft Docs"
description: "Descripción de la solución preconfigurada de mantenimiento predictivo del Conjunto de aplicaciones de IoT de Azure."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="48334-103">Información general de la solución preconfigurada de mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="48334-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="48334-104">La [solución preconfigurada][lnk_preconfigured_solutions] de *mantenimiento predictivo* es una de las soluciones preconfiguradas del [Conjunto de aplicaciones de IoT de Microsoft Azure][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="48334-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="48334-105">Esta solución integra la colección de telemetría del dispositivo en tiempo real con un modelo predictivo creado mediante [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="48334-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="48334-106">Con el Conjunto de aplicaciones de IoT de Azure, puede conectarse de forma rápida y fácil a los recursos, supervisarlos y analizar datos en tiempo real en paneles y visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="48334-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="48334-107">En la solución de mantenimiento predictivo, las visualizaciones y paneles le proporcionan una nueva inteligencia que puede impulsar las eficiencias y mejorar los flujos de ingresos.</span><span class="sxs-lookup"><span data-stu-id="48334-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="48334-108">Escenario</span><span class="sxs-lookup"><span data-stu-id="48334-108">The Scenario</span></span>

<span data-ttu-id="48334-109">Fabrikam es una compañía de líneas aéreas regional que se centra en la fantástica experiencia del cliente en los precios competitivos.</span><span class="sxs-lookup"><span data-stu-id="48334-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="48334-110">Una causa de los retrasos en los vuelos son los problemas de mantenimiento y el mantenimiento de los motores de los aviones supone especialmente un desafío.</span><span class="sxs-lookup"><span data-stu-id="48334-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="48334-111">Fabrikam debe evitar los errores en los motores durante el vuelo a toda costa, por lo que inspecciona sus motores con regularidad y se ajusta a un programa de mantenimiento programado.</span><span class="sxs-lookup"><span data-stu-id="48334-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="48334-112">Sin embargo, los motores de aviones no siempre llevan el mismo.</span><span class="sxs-lookup"><span data-stu-id="48334-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="48334-113">En los motores se realizan algunas tareas de mantenimiento innecesarias.</span><span class="sxs-lookup"><span data-stu-id="48334-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="48334-114">Lo que es aún más importante, surgen problemas que pueden hacer que un avión quede inmovilizado hasta que se realice el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="48334-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="48334-115">Si un avión está en una ubicación donde no se encuentran disponibles los técnicos o las piezas de repuesto adecuados, estos problemas pueden resultar muy costosos.</span><span class="sxs-lookup"><span data-stu-id="48334-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="48334-116">Los motores de los aviones de Fabrikam están equipados con sensores que supervisan las condiciones del motor durante el vuelo.</span><span class="sxs-lookup"><span data-stu-id="48334-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="48334-117">Fabrikam utiliza la solución de mantenimiento predictivo para recopilar los datos del sensor recopilados durante el vuelo.</span><span class="sxs-lookup"><span data-stu-id="48334-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="48334-118">Tras años de acumular datos de errores y de funcionamiento del motor, los científicos de datos de Fabrikam han modelado una manera de predecir la vida útil restante (RUL) del motor de un avión.</span><span class="sxs-lookup"><span data-stu-id="48334-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="48334-119">El modelo emplea una correlación entre los datos de cuatro de los sensores del motor con el desgaste del motor que lleva a averías ocasionales.</span><span class="sxs-lookup"><span data-stu-id="48334-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="48334-120">Mientras Fabrikam continúa realizando inspecciones periódicas para garantizar la seguridad, ahora puede usar los modelos para calcular el RUL de cada motor después de cada vuelo.</span><span class="sxs-lookup"><span data-stu-id="48334-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="48334-121">El modelo usa la telemetría recopilada por los motores durante el vuelo.</span><span class="sxs-lookup"><span data-stu-id="48334-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="48334-122">Fabrikam puede predecir ahora de antemano los puntos futuros de error y el plan de mantenimiento y reparación.</span><span class="sxs-lookup"><span data-stu-id="48334-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="48334-123">El modelo de solución utiliza datos de desgaste del motor reales.</span><span class="sxs-lookup"><span data-stu-id="48334-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="48334-124">Al predecir el punto en el que se requiere mantenimiento, Fabrikam puede optimizar sus operaciones para reducir los costos.</span><span class="sxs-lookup"><span data-stu-id="48334-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="48334-125">Los coordinadores de mantenimiento trabajan con programadores para:</span><span class="sxs-lookup"><span data-stu-id="48334-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="48334-126">Planear el mantenimiento de forma que coincida con la parada de un avión en una ubicación concreta.</span><span class="sxs-lookup"><span data-stu-id="48334-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="48334-127">Asegurarse de que el avión esté fuera de servicio el tiempo suficiente sin provocar interrupciones en la programación.</span><span class="sxs-lookup"><span data-stu-id="48334-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="48334-128">Para programar a los técnicos de forma que se tenga la seguridad de que el avión es revisado de forma eficiente sin tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="48334-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="48334-129">Los administradores del control de inventario reciben planes de mantenimiento para poder optimizar su proceso de realización de pedidos y el inventario de las piezas de repuesto.</span><span class="sxs-lookup"><span data-stu-id="48334-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="48334-130">Todas estas actividades permiten a Fabrikam minimizar el tiempo de permanencia en tierra de los aviones y reducir los costos operativos a la vez que se garantizan la seguridad de los pasajeros y de la tripulación.</span><span class="sxs-lookup"><span data-stu-id="48334-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="48334-131">Para entender la manera en que el [Conjunto de aplicaciones de IoT de Azure][lnk_iot_suite] ofrece las funcionalidades que los clientes necesitan para alcanzar el potencial del mantenimiento predictivo, consulte esta [infografía][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="48334-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="48334-132">Cómo se crea la solución de un mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="48334-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="48334-133">La solución aprovecha un modelo de Azure Machine Learning existente disponible como plantilla para mostrar cómo actúan estas funcionalidades a partir de la telemetría del dispositivo recopilada mediante los servicios del Conjunto de aplicaciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="48334-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="48334-134">Microsoft ha creado un [modelo de regresión][lnk_regression_model] de un motor de avión basado en los datos disponibles públicamente<sup>\[1\]</sup> y las instrucciones paso a paso sobre cómo utilizar el modelo.</span><span class="sxs-lookup"><span data-stu-id="48334-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="48334-135">La solución de mantenimiento predictivo de Azure IoT usa el modelo de regresión creado a partir de esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="48334-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="48334-136">El modelo se implementa en la suscripción de Azure y se expone mediante una API generada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="48334-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="48334-137">La solución incluye un subconjunto de los datos de prueba que representa 4 motores (de un total de 100) y 4 flujos de datos de sensor (de un total de 21).</span><span class="sxs-lookup"><span data-stu-id="48334-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="48334-138">Estos datos son suficientes para proporcionar un resultado preciso del modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="48334-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="48334-139">*\[1\] A. Saxena and K. Goebel (2008). "Conjunto de datos de simulación de degradación del motor de turbofán", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="48334-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="48334-140">Introducción al mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="48334-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="48334-141">En este tutorial se muestra cómo aprovisionar la solución de mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="48334-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="48334-142">También le lleva por las características básicas de la solución de mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="48334-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="48334-143">Puede acceder a muchas de estas características mediante el panel de soluciones que se implementa junto con la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="48334-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="48334-144">Para completar este tutorial, deberá tener una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="48334-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="48334-145">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="48334-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="48334-146">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="48334-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="48334-147">Inicie sesión en [azureiotsuite.com][lnk-azureiotsuite] con sus credenciales de la cuenta de Azure y haga clic en **+** para crear una nueva solución.</span><span class="sxs-lookup"><span data-stu-id="48334-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="48334-148">Haga clic en **Seleccionar** en el icono de **Mantenimiento predictivo**.</span><span class="sxs-lookup"><span data-stu-id="48334-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="48334-149">Escriba un **nombre** para la solución preconfigurada de mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="48334-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="48334-150">Seleccione la **región** y la **suscripción** que desea usar para aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="48334-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="48334-151">Haga clic en **Crear solución** para comenzar el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="48334-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="48334-152">Este proceso normalmente tarda varios minutos en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="48334-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="48334-153">Espere a que se complete el proceso de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="48334-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="48334-154">Haga clic en el icono de la solución con el estado **Aprovisionando**.</span><span class="sxs-lookup"><span data-stu-id="48334-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="48334-155">Observe los **estados de aprovisionamiento** , ya que los servicios de Azure se implementan en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="48334-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="48334-156">Una vez que se complete el aprovisionamiento, el estado cambia a **Listo**.</span><span class="sxs-lookup"><span data-stu-id="48334-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="48334-157">Haga clic en el icono y verá los detalles de la solución en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="48334-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="48334-158">En este panel, puede iniciar el panel de soluciones y acceder al área de trabajo de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="48334-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="48334-159">Si surgen problemas al implementar la solución preconfigurada, revise las secciones [Permisos en el sitio azureiotsuite.com][lnk-permissions] y [Preguntas más frecuentes][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="48334-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="48334-160">Si los problemas persisten, cree un vale de servicio en el [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="48334-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="48334-161">¿Hay detalles que esperaría ver que no aparezcan para su solución?</span><span class="sxs-lookup"><span data-stu-id="48334-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="48334-162">Puede sugerirnos nuevas características en [User Voice](https://feedback.azure.com/forums/321918-azure-iot)(La voz del usuario).</span><span class="sxs-lookup"><span data-stu-id="48334-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="48334-163">Visualización de la solución</span><span class="sxs-lookup"><span data-stu-id="48334-163">View the solution</span></span>

<span data-ttu-id="48334-164">Esta sección le guía por la interfaz de usuario de la solución.</span><span class="sxs-lookup"><span data-stu-id="48334-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="48334-165">Panel de mantenimiento predictivo </span><span class="sxs-lookup"><span data-stu-id="48334-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="48334-166">Esta página de la aplicación web utiliza controles de Power BI JavaScript (consulte el [repositorio de imágenes de Power BI][lnk-powerbi]) para ver:</span><span class="sxs-lookup"><span data-stu-id="48334-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="48334-167">Los datos de salida de los trabajos de Análisis de transmisiones en el Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="48334-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="48334-168">El recuento de ciclos y la vida útil restante por cada motor de avión.</span><span class="sxs-lookup"><span data-stu-id="48334-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="48334-169">Observación del comportamiento de la solución en la nube</span><span class="sxs-lookup"><span data-stu-id="48334-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="48334-170">En el Portal de Azure, desplácese al grupo de recursos con el nombre de la solución elegida para poder ver los recursos aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="48334-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="48334-171">Al aprovisionar la solución preconfigurada, recibirá un mensaje de correo electrónico con un vínculo al área de trabajo de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="48334-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="48334-172">También puede navegar al área de trabajo de Machine Learning desde la página [azureiotsuite.com][lnk-azureiotsuite] de la solución de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="48334-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="48334-173">Hay un icono disponible en esta página cuando la solución se encuentra en el estado **Listo**.</span><span class="sxs-lookup"><span data-stu-id="48334-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="48334-174">En el portal de la solución, puede ver que el ejemplo se aprovisiona con cuatro dispositivos simulados que representan dos aviones con dos motores por avión y cuatro sensores por motor.</span><span class="sxs-lookup"><span data-stu-id="48334-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="48334-175">Cuando va al portal de la solución por primera vez, se detiene la simulación.</span><span class="sxs-lookup"><span data-stu-id="48334-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="48334-176">Haga clic en **Iniciar simulación** para empezar la simulación.</span><span class="sxs-lookup"><span data-stu-id="48334-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="48334-177">El historial del sensor, la vida útil restante, los ciclos y el historial de vida útil restante rellenan con datos el panel.</span><span class="sxs-lookup"><span data-stu-id="48334-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="48334-178">Si la vida útil restante es inferior a 160 (un umbral arbitrario elegido para fines de demostración), el portal de la solución muestra un símbolo de advertencia junto a la presentación de la vida útil restante.</span><span class="sxs-lookup"><span data-stu-id="48334-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="48334-179">El portal de la solución también resalta en amarillo el motor del avión.</span><span class="sxs-lookup"><span data-stu-id="48334-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="48334-180">Observe cómo los valores de la vida útil restante presentan una tendencia descendente en general pero tienden a rebotar hacia arriba y hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="48334-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="48334-181">Este comportamiento es consecuencia de las longitudes del ciclo que varían y de la precisión del modelo.</span><span class="sxs-lookup"><span data-stu-id="48334-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="48334-182">La simulación completa tarda alrededor de 35 minutos en finalizar 148 ciclos.</span><span class="sxs-lookup"><span data-stu-id="48334-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="48334-183">Se alcanza el umbral de vida útil restante de 160 por primera vez en unos 5 minutos y ambos motores alcanzan el umbral en aproximadamente unos 8 minutos.</span><span class="sxs-lookup"><span data-stu-id="48334-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="48334-184">La simulación ejecuta el conjunto de datos completo para 148 ciclos y se establece en los valores finales de la vida útil existente y de ciclos.</span><span class="sxs-lookup"><span data-stu-id="48334-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="48334-185">Puede detener la simulación en cualquier punto, pero al hacer clic en **Iniciar simulación** se reproduce la simulación desde el principio del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="48334-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48334-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48334-186">Next steps</span></span>

<span data-ttu-id="48334-187">Para más información acerca de cómo IoT de Azure habilita escenarios de mantenimiento predictivo, lea el documento sobre [Captura del valor de Internet de las cosas][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="48334-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="48334-188">Examine el [tutorial][lnk-predictive-walkthrough] de la solución de mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="48334-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="48334-189">También puede explorar algunas de las demás características y funcionalidades de las soluciones preconfiguradas del conjunto de aplicaciones de IoT:</span><span class="sxs-lookup"><span data-stu-id="48334-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="48334-190">[Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="48334-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="48334-191">[Seguridad de Internet de las cosas desde el principio][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="48334-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/