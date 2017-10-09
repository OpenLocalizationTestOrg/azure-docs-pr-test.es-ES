---
title: "mantenimiento aaaPredictive preconfigurado solución | Documentos de Microsoft"
description: "Una descripción de un mantenimiento predictivo hello Azure IoT conjunto preconfigurado de solución."
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
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="aa881-103">Información general de la solución preconfigurada de mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="aa881-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="aa881-104">Hola *mantenimiento predictivo* [preconfigurado solución] [ lnk_preconfigured_solutions] es uno de hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="aa881-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="aa881-105">Esta solución integra la colección de telemetría del dispositivo en tiempo real con un modelo predictivo creado mediante [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="aa881-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="aa881-106">Con el conjunto de IoT de Azure, puede rápidamente y fácilmente conectarse tooand activos de monitor y analizar la telemetría en tiempo real en los paneles y las visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="aa881-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="aa881-107">En la solución de un mantenimiento predictivo hello, visualizaciones y los paneles de hello proporcionan nueva inteligencia que puede impulsar las eficiencias y mejorar los flujos de ingresos.</span><span class="sxs-lookup"><span data-stu-id="aa881-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="aa881-108">Hola escenario</span><span class="sxs-lookup"><span data-stu-id="aa881-108">hello Scenario</span></span>

<span data-ttu-id="aa881-109">Fabrikam es una compañía de líneas aéreas regional que se centra en la fantástica experiencia del cliente en los precios competitivos.</span><span class="sxs-lookup"><span data-stu-id="aa881-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="aa881-110">Una causa de los retrasos en los vuelos son los problemas de mantenimiento y el mantenimiento de los motores de los aviones supone especialmente un desafío.</span><span class="sxs-lookup"><span data-stu-id="aa881-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="aa881-111">Fabrikam debe evitar el error del motor durante el vuelo a toda costa, así que inspecciona sus motores con regularidad y programa según tooa plan de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="aa881-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="aa881-112">Sin embargo, siempre no usan motores de avión Hola igual.</span><span class="sxs-lookup"><span data-stu-id="aa881-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="aa881-113">En los motores se realizan algunas tareas de mantenimiento innecesarias.</span><span class="sxs-lookup"><span data-stu-id="aa881-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="aa881-114">Lo que es aún más importante, surgen problemas que pueden hacer que un avión quede inmovilizado hasta que se realice el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="aa881-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="aa881-115">Si un avión está en una ubicación donde Hola derecho técnicos o piezas de recambio no están disponibles, estos problemas pueden ser especialmente costosos.</span><span class="sxs-lookup"><span data-stu-id="aa881-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="aa881-116">motores de Hola de avión de Fabrikam se instrumentan con sensores que supervisan las condiciones del motor durante el tránsito.</span><span class="sxs-lookup"><span data-stu-id="aa881-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="aa881-117">Fabrikam utiliza Hola mantenimiento predictivo solución toocollect Hola sensor datos recopilados durante la caja de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="aa881-118">Después de acumular años de funcionamiento del motor y datos de error, científicos de datos de Fabrikam modelan un hello toopredict de manera vida útil restante (RUL) de un motor de avión.</span><span class="sxs-lookup"><span data-stu-id="aa881-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="aa881-119">modelo de Hello usa una correlación entre los datos de cuatro de sensores de motor de Hola y desgaste motor que provoca el error tooeventual.</span><span class="sxs-lookup"><span data-stu-id="aa881-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="aa881-120">Mientras Fabrikam continúa tooensure seguridad de tooperform inspecciones periódicas, ahora puede usar Hola modelos toocompute Hola RUL para cada motor después de cada vuelo.</span><span class="sxs-lookup"><span data-stu-id="aa881-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="aa881-121">modelo de Hello usa telemetría Hola recopilada de los motores de Hola durante el vuelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="aa881-122">Fabrikam puede predecir ahora de antemano los puntos futuros de error y el plan de mantenimiento y reparación.</span><span class="sxs-lookup"><span data-stu-id="aa881-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="aa881-123">modelo de solución de Hello usa datos de uso reales del motor.</span><span class="sxs-lookup"><span data-stu-id="aa881-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="aa881-124">Al predecir punto hello cuando se requiere mantenimiento, Fabrikam puede optimizar el costo que implica operaciones tooreduce.</span><span class="sxs-lookup"><span data-stu-id="aa881-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="aa881-125">Los coordinadores de mantenimiento trabajan con programadores para:</span><span class="sxs-lookup"><span data-stu-id="aa881-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="aa881-126">Plan de mantenimiento toocoincide con un avión detener en una ubicación concreta.</span><span class="sxs-lookup"><span data-stu-id="aa881-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="aa881-127">Asegúrese de que el tiempo suficiente está disponible para hello avión toobe fuera de servicio sin causar interrupciones de programación.</span><span class="sxs-lookup"><span data-stu-id="aa881-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="aa881-128">tooschedule tooensure de técnicos que avión se atiende de forma eficaz sin tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="aa881-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="aa881-129">Los administradores del control de inventario reciben planes de mantenimiento para poder optimizar su proceso de realización de pedidos y el inventario de las piezas de repuesto.</span><span class="sxs-lookup"><span data-stu-id="aa881-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="aa881-130">Estas actividades habilitar hora de tierra de Fabrikam toominimize avión y reducen los costos operativos al garantizar la seguridad de Hola de pasajeros y personal.</span><span class="sxs-lookup"><span data-stu-id="aa881-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="aa881-131">toounderstand cómo [Azure IoT Suite] [ lnk_iot_suite] proporciona capacidades de hello los clientes necesitan potencial de hello toorealize del mantenimiento predictivo, revise esta [infografía] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="aa881-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="aa881-132">Cómo se crea la solución de un mantenimiento predictivo Hola</span><span class="sxs-lookup"><span data-stu-id="aa881-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="aa881-133">solución de Hello utiliza un modelo de aprendizaje automático de Azure existente disponible como una plantilla tooshow estas capacidades trabajar de telemetría de dispositivo que se recopilan a través de servicios IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="aa881-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="aa881-134">Microsoft ha creado un [modelo de regresión] [ lnk_regression_model] de un motor de avión basándose en los datos disponibles públicamente<sup>\[1\]</sup>y paso a paso instrucciones sobre cómo toouse Hola modelo.</span><span class="sxs-lookup"><span data-stu-id="aa881-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="aa881-135">Hola solución de un mantenimiento predictivo IoT de Azure usa el modelo de regresión de hello creado desde esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="aa881-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="aa881-136">modelo de Hello es implementado en su suscripción de Azure y se expone a través de una API generada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aa881-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="aa881-137">solución de Hello incluye un subconjunto de datos que representa 4 (del total de 100) de prueba de hello motores y secuencias de datos del sensor de hello 4 (de 21 total).</span><span class="sxs-lookup"><span data-stu-id="aa881-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="aa881-138">Estos datos son suficiente tooprovide un resultado exacto del modelo entrenado Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="aa881-139">*\[1\] A. Saxena and K. Goebel (2008). "Conjunto de datos de simulación de degradación del motor de turbofán", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="aa881-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="aa881-140">Introducción al mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="aa881-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="aa881-141">Este tutorial muestra cómo tooprovision Hola solución mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="aa881-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="aa881-142">También le guía a través de características básicas de Hola de solución de un mantenimiento predictivo Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="aa881-143">Puede tener acceso a muchas de estas características a través del panel de la solución de Hola que implementa junto con la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="aa881-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="aa881-144">toocomplete este tutorial, necesita una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa881-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="aa881-145">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="aa881-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="aa881-146">Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="aa881-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="aa881-147">Inicie sesión demasiado[azureiotsuite.com] [ lnk-azureiotsuite] con Azure credenciales de cuenta y haga clic en  **+**  toocreate una solución.</span><span class="sxs-lookup"><span data-stu-id="aa881-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="aa881-148">Haga clic en **seleccione** hello **mantenimiento predictivo** icono.</span><span class="sxs-lookup"><span data-stu-id="aa881-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="aa881-149">Escriba un **nombre** para la solución preconfigurada de mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="aa881-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="aa881-150">Seleccione hello **región** y **suscripción** desea toouse tooprovision Hola solución.</span><span class="sxs-lookup"><span data-stu-id="aa881-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="aa881-151">Haga clic en **crear solución** hello toobegin proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="aa881-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="aa881-152">Este proceso suele tarda varios toorun minutos.</span><span class="sxs-lookup"><span data-stu-id="aa881-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="aa881-153">Espere hello toocomplete del proceso de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="aa881-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="aa881-154">Haga clic en el icono de hello para la solución con **Provisioning** estado.</span><span class="sxs-lookup"><span data-stu-id="aa881-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="aa881-155">Hola aviso **aprovisionamiento estados** tal y como se implementan los servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa881-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="aa881-156">Una vez que finalice el aprovisionamiento, Hola cambios de estado demasiado**listo**.</span><span class="sxs-lookup"><span data-stu-id="aa881-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="aa881-157">Haga clic en detalles del hello toosee Hola icono de la solución en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="aa881-158">En este panel, puede iniciar Hola solución panel y acceso Hola aprendizaje automático área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="aa881-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="aa881-159">Si encuentra problemas al implementar soluciones de hello preconfigurado, consulte [permisos en el sitio de hello azureiotsuite.com] [ lnk-permissions] hello y [preguntas más frecuentes sobre] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="aa881-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="aa881-160">Si continúan los problemas de hello, crear un vale de servicio en hello [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="aa881-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="aa881-161">¿Hay detalles que se esperaría toosee que no aparezcan para su solución?</span><span class="sxs-lookup"><span data-stu-id="aa881-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="aa881-162">Puede sugerirnos nuevas características en [User Voice](https://feedback.azure.com/forums/321918-azure-iot)(La voz del usuario).</span><span class="sxs-lookup"><span data-stu-id="aa881-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="aa881-163">Solución de hello de vista</span><span class="sxs-lookup"><span data-stu-id="aa881-163">View hello solution</span></span>

<span data-ttu-id="aa881-164">Esta sección le guía a través de la solución de hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="aa881-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="aa881-165">Panel de mantenimiento predictivo </span><span class="sxs-lookup"><span data-stu-id="aa881-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="aa881-166">Esta página de aplicación web de hello usa controles de PowerBI JavaScript (vea hello [repositorio de PowerBI-visuals][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="aa881-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="aa881-167">datos de salida de Hello de trabajos de análisis de transmisiones de hello en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="aa881-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="aa881-168">Hola RUL y ciclo de recuento por el motor de avión.</span><span class="sxs-lookup"><span data-stu-id="aa881-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="aa881-169">Observar el comportamiento de Hola de solución de nube de Hola</span><span class="sxs-lookup"><span data-stu-id="aa881-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="aa881-170">En la consulta Hola portal de Azure, navegue toohello grupo de recursos con nombre de la solución de hello eligió tooview los recursos aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="aa881-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="aa881-171">Al aprovisionar solución Hola preconfigurado, recibirá un correo electrónico con un área de trabajo de aprendizaje automático de toohello de vínculo.</span><span class="sxs-lookup"><span data-stu-id="aa881-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="aa881-172">También puede navegar el área de trabajo de aprendizaje automático de toohello de hello [azureiotsuite.com] [ lnk-azureiotsuite] página para su solución de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="aa881-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="aa881-173">Un icono está disponible en esta página cuando la solución de Hola Hola **listo** estado.</span><span class="sxs-lookup"><span data-stu-id="aa881-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="aa881-174">En el portal de solución de hello, puede ver que ese ejemplo Hola está proporcionado de avión de dos dispositivos simulados cuatro toorepresent con dos motores por avión, cada uno con cuatro sensores.</span><span class="sxs-lookup"><span data-stu-id="aa881-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="aa881-175">Cuando desplace portal de solución de toohello por primera vez, se ha detenido simulación de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="aa881-176">Haga clic en **iniciar simulación** simulación de hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="aa881-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="aa881-177">Hola historial de sensor, RUL, ciclos y RUL historial rellenar panel Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="aa881-178">Cuando RUL es inferior a 160 (un umbral arbitrario elegido para fines de demostración), portal de solución de hello muestra un toohello siguiente de símbolo de advertencia RUL mostrar.</span><span class="sxs-lookup"><span data-stu-id="aa881-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="aa881-179">portal de solución de Hello también resalta el motor de avión de hello en amarillo.</span><span class="sxs-lookup"><span data-stu-id="aa881-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="aa881-180">Observe cómo los valores de hello RUL tienen una tendencia hacia abajo general general, pero suelen toobounce arriba y abajo.</span><span class="sxs-lookup"><span data-stu-id="aa881-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="aa881-181">Este comportamiento da como resultado de diversas longitudes de ciclo de Hola y precisión del modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="aa881-182">simulación completa de Hello tarda aproximadamente 35 toocomplete minutos 148 ciclos.</span><span class="sxs-lookup"><span data-stu-id="aa881-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="aa881-183">umbral de Hello 160 RUL se cumple para hello primera vez en unos 5 minutos y dos motores ha alcanzado el umbral de hello en aproximadamente 8 minutos.</span><span class="sxs-lookup"><span data-stu-id="aa881-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="aa881-184">simulación de Hola se ejecuta a través del conjunto de datos completo de Hola para 148 ciclos y abona en valores finales RUL y ciclo.</span><span class="sxs-lookup"><span data-stu-id="aa881-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="aa881-185">Puede detener la simulación de Hola en cualquier punto, pero al hacer clic en **iniciar simulación** las reproducciones Hola simulación desde el principio de hello del conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa881-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa881-186">Next steps</span></span>

<span data-ttu-id="aa881-187">más información acerca de cómo IoT de Azure permite escenarios de un mantenimiento predictivo, leer toolearn [capturar el valor de Internet de las cosas hello][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="aa881-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="aa881-188">Tomar una [tutorial] [ lnk-predictive-walkthrough] de solución de un mantenimiento predictivo Hola.</span><span class="sxs-lookup"><span data-stu-id="aa881-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="aa881-189">También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:</span><span class="sxs-lookup"><span data-stu-id="aa881-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="aa881-190">[Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="aa881-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="aa881-191">[Seguridad de IoT de hello masa][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="aa881-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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