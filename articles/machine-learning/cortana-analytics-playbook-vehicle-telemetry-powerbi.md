---
title: "transformación de aaaPower panel de BI para mantenimiento de vehículo y dirigir - Azure | Documentos de Microsoft"
description: "Usar funciones de Hola de toogain en tiempo real y predicción visión de inteligencia de Cortana en el estado del vehículo y dirigir hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="99a60-103">Instrucciones de configuración del panel de Power BI para la plantilla de la solución Análisis de telemetría de vehículos</span><span class="sxs-lookup"><span data-stu-id="99a60-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="99a60-104">Esto **menú** vincula toohello capítulos en esta guía.</span><span class="sxs-lookup"><span data-stu-id="99a60-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="99a60-105">Hola solución de análisis de telemetría de vehículo muestra cómo concesiones de coches, los fabricantes de automóviles y compañías de seguros pueden aprovechar las capacidades de Hola de inteligencia de Cortana toogain en tiempo real y predicción obtener información detallada en el mantenimiento de vehículo y dirigir las mejoras del toodrive hábitos de cliente en el área de hello experiencia, departamento de I+d y campañas de marketing.</span><span class="sxs-lookup"><span data-stu-id="99a60-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="99a60-106">Este documento contiene instrucciones paso a paso acerca de cómo puede configurar informes de Power BI de Hola y el panel una vez implementada la solución hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="99a60-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="99a60-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99a60-107">Prerequisites</span></span>
1. <span data-ttu-id="99a60-108">Implementar hello [análisis de telemetría](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solución</span><span class="sxs-lookup"><span data-stu-id="99a60-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="99a60-109">Instalar Microsoft Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="99a60-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="99a60-110">Una [suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99a60-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="99a60-111">Si no tiene una suscripción de Azure, comience con una suscripción gratis de Azure.</span><span class="sxs-lookup"><span data-stu-id="99a60-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="99a60-112">Cuenta de Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="99a60-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="99a60-113">Componentes de Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="99a60-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="99a60-114">Como parte de la plantilla de solución de análisis de telemetría de vehículo hello, Hola después de los servicios de inteligencia de Cortana se implementa en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="99a60-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="99a60-115">**Centro de eventos** para la introducción de millones de eventos de telemetría del vehículo en Azure.</span><span class="sxs-lookup"><span data-stu-id="99a60-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="99a60-116">**Análisis de transmisiones** para obtener información en tiempo real sobre el estado del vehículo y conserva los datos en el almacenamiento a largo plazo para análisis de lotes más completo.</span><span class="sxs-lookup"><span data-stu-id="99a60-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="99a60-117">**Aprendizaje automático** para la detección de anomalías en tiempo real y toogain predictiva visión de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="99a60-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="99a60-118">**HDInsight** tootransform aprovechado datos a escala</span><span class="sxs-lookup"><span data-stu-id="99a60-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="99a60-119">**Factoría de datos** controla la orquestación, programación, administración de recursos y la supervisión de la canalización de procesamiento por lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="99a60-120">**Power BI** ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="99a60-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="99a60-121">solución de Hello utiliza dos orígenes de datos diferentes: **simulan las señales de vehículo y conjunto de datos de diagnóstico** y **catálogo vehículo**.</span><span class="sxs-lookup"><span data-stu-id="99a60-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="99a60-122">Se incluye un simulador telemático del vehículo como parte de esta solución.</span><span class="sxs-lookup"><span data-stu-id="99a60-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="99a60-123">Se emite información de diagnóstico y señales de estado toohello correspondiente del vehículo hello y conducir patrón en un momento dado en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="99a60-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="99a60-124">Hello vehículo catálogo es una asignación referencia conjunto de datos que contienen Niv toomodel</span><span class="sxs-lookup"><span data-stu-id="99a60-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="99a60-125">Preparación de panel de Power BI</span><span class="sxs-lookup"><span data-stu-id="99a60-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="99a60-126">Configuración del panel de Power BI en tiempo real</span><span class="sxs-lookup"><span data-stu-id="99a60-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="99a60-127">**Iniciar la aplicación de panel en tiempo real de hello** cuando se haya completado la implementación de hello, debe seguir las instrucciones de funcionamiento de hello Manual</span><span class="sxs-lookup"><span data-stu-id="99a60-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="99a60-128">Descargue la aplicación de panel en tiempo real RealtimeDashboardApp.zip y descomprímala.</span><span class="sxs-lookup"><span data-stu-id="99a60-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="99a60-129">En la carpeta descomprimida de hello, abra el archivo de configuración de aplicación 'RealtimeDashboardApp.exe.config' appSettings de reemplazo para las conexiones de servicio de Eventhub, almacenamiento de blobs y aprendizaje automático con valores de hello en hello Manual de las instrucciones de funcionamiento y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="99a60-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="99a60-130">Ejecute la aplicación RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="99a60-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="99a60-131">Una ventana de inicio de sesión se emergente, proporcione sus credenciales de Power BI válidos y haga clic en hello **Accept** botón.</span><span class="sxs-lookup"><span data-stu-id="99a60-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="99a60-132">A continuación, la aplicación hello iniciará toorun.</span><span class="sxs-lookup"><span data-stu-id="99a60-132">Then hello app will start toorun.</span></span>

   ![Inicio de sesión tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Permisos de panel de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="99a60-135">Sitio Web de tooPowerBI de inicio de sesión y crear un panel en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="99a60-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="99a60-136">Ahora, está listo tooconfigure panel de Power BI Hola con toogain visualizaciones enriquecidas en tiempo real y transformación de la visión de predicción en mantenimiento de vehículo y dirigir.</span><span class="sxs-lookup"><span data-stu-id="99a60-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="99a60-137">Tardará aproximadamente 45 minutos tooan hora toocreate Hola todos los informes y configurar panel Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="99a60-138">Configuración de informes de Power BI</span><span class="sxs-lookup"><span data-stu-id="99a60-138">Configure Power BI reports</span></span>
<span data-ttu-id="99a60-139">informes en tiempo real de Hola y el panel de hello tardan aproximadamente toocomplete 30 y 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="99a60-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="99a60-140">Examinar demasiado[http://powerbi.com](http://powerbi.com) e inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99a60-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Inicio de sesión tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="99a60-142">Se genera un nuevo conjunto de datos en Power BI.</span><span class="sxs-lookup"><span data-stu-id="99a60-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="99a60-143">Haga clic en hello **ConnectedCarsRealtime** conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="99a60-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Seleccione conjunto de datos en tiempo real de automóviles conectados.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="99a60-145">Guardar informe en blanco de hello mediante **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="99a60-145">Save hello blank report using **Ctrl + s**.</span></span>

![Guardar el informe en blanco](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="99a60-147">Proporcione el nombre del informe *Análisis de telemetría del vehículo en tiempo real - Informes*.</span><span class="sxs-lookup"><span data-stu-id="99a60-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Proporcione el nombre del informe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="99a60-149">Informes en tiempo real</span><span class="sxs-lookup"><span data-stu-id="99a60-149">Real-time reports</span></span>
<span data-ttu-id="99a60-150">Hay tres informes en tiempo real en esta solución:</span><span class="sxs-lookup"><span data-stu-id="99a60-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="99a60-151">Vehículos en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="99a60-151">Vehicles in operation</span></span>
2. <span data-ttu-id="99a60-152">Vehículos que requieren mantenimiento</span><span class="sxs-lookup"><span data-stu-id="99a60-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="99a60-153">Estadísticas de estado de los vehículos</span><span class="sxs-lookup"><span data-stu-id="99a60-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="99a60-154">Puede elegir tooconfigure todos los informes en tiempo real tres de Hola o detenerse después de cualquier fase y continuar toohello la siguiente sección de configuración de informes de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="99a60-155">Le recomendamos que todos los toocreate Hola tres informes visión completa de hello toovisualize de ruta de acceso en tiempo real de Hola de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="99a60-156">1. Vehículos en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="99a60-156">1. Vehicles in operation</span></span>
<span data-ttu-id="99a60-157">Haga doble clic en **página 1** y cambie su nombre demasiado "Vehículos en la operación"</span><span class="sxs-lookup"><span data-stu-id="99a60-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="99a60-158">![Automóviles conectados: Vehículos en funcionamiento](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="99a60-159">Seleccione el campo **vin** en **Campos** y elija el tipo de visualización como **“Tarjeta”**.</span><span class="sxs-lookup"><span data-stu-id="99a60-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="99a60-160">Se crea la visualización de tarjeta como se muestra en la ilustración.</span><span class="sxs-lookup"><span data-stu-id="99a60-160">Card visualization is created as shown in figure.</span></span>  
    ![Automóviles conectados - Seleccionar vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="99a60-162">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-163">Seleccione **city** y **vin** en los campos.</span><span class="sxs-lookup"><span data-stu-id="99a60-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="99a60-164">Cambiar visualización demasiado**"Map"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="99a60-165">Arrastre **vin** al área de valores.</span><span class="sxs-lookup"><span data-stu-id="99a60-165">Drag **vin** in values area.</span></span> <span data-ttu-id="99a60-166">Arrastre **city** de campos demasiado**leyenda** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="99a60-167">![Automóviles conectados - Visualización de tarjeta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="99a60-168">Seleccione **formato** sección **visualizaciones**, haga clic en **título** y cambiar hello **texto** demasiado**"vehículos en operación por ciudad"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="99a60-169">![Automóviles conectados: Vehículos en funcionamiento por ciudad](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="99a60-170">La visualización final tiene el aspecto que se muestra en la ilustración.</span><span class="sxs-lookup"><span data-stu-id="99a60-170">Final visualization looks as shown in figure.</span></span>    
    ![Automóviles conectados - Visualización final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="99a60-172">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-173">Seleccione **City** y **Niv**, cambie el tipo de visualización demasiado**gráfico de columnas agrupadas**.</span><span class="sxs-lookup"><span data-stu-id="99a60-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="99a60-174">Asegúrese de que el campo **city** esté en el área **Eje** y **vin** en el área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="99a60-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="99a60-175">Ordene el gráfico por **“Recuento de vin”**.</span><span class="sxs-lookup"><span data-stu-id="99a60-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="99a60-176">![Automóviles conectados - Recuento de vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="99a60-177">Gráfico de cambio **título** demasiado**"Vehículos en operación por ciudad"**</span><span class="sxs-lookup"><span data-stu-id="99a60-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="99a60-178">Haga clic en hello **formato** sección, a continuación, seleccione **colores de datos**, haga clic en hello **"En"** demasiado**mostrar todo**</span><span class="sxs-lookup"><span data-stu-id="99a60-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="99a60-179">![Automóviles conectados: Mostrar todos los colores de datos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="99a60-180">Cambiar el color de Hola de ciudad individual haciendo clic en el icono de color.</span><span class="sxs-lookup"><span data-stu-id="99a60-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Automóviles conectados - Cambiar colores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="99a60-182">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-183">Seleccione la visualización **Gráfico de columnas agrupadas** en Visualizaciones, arrastre el campo **city** al área **Eje**, el campo **Model** al área **Leyenda** y el campo **vin** al área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="99a60-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="99a60-184">![Automóviles conectados: Gráfico de columnas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="99a60-185">![Automóviles conectados: Representación](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="99a60-186">Reorganice toda la visualización de esta página como se muestra en la ilustración.</span><span class="sxs-lookup"><span data-stu-id="99a60-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Automóviles conectados - Visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="99a60-188">Informes en tiempo real de Hola "Vehículos en la operación" se configuró correctamente.</span><span class="sxs-lookup"><span data-stu-id="99a60-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="99a60-189">Puede continuar informes en tiempo real de toocreate Hola siguiente o deténgase aquí y configuración de panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="99a60-190">2. Vehículos que requieren mantenimiento</span><span class="sxs-lookup"><span data-stu-id="99a60-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="99a60-191">Haga clic en ![agregar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd un nuevo informe, cámbiele el nombre demasiado**"Vehículos que requieren mantenimiento"**</span><span class="sxs-lookup"><span data-stu-id="99a60-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Automóviles conectados - Vehículos que requieren mantenimiento](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="99a60-193">Seleccione **Niv** del campo y cambiar el tipo de visualización demasiado**tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="99a60-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="99a60-194">![Automóviles conectados: Visualización de tarjeta vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="99a60-195">Tenemos un campo denominado "MaintenanceLabel" en el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="99a60-196">Este campo puede tener un valor de "0" o "1".</span><span class="sxs-lookup"><span data-stu-id="99a60-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="99a60-197">Se establece mediante el modelo de aprendizaje automático de Azure Hola suministrados como parte de la solución y se integran con la ruta de acceso en tiempo real de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="99a60-198">valor de Hola "1" indica que un vehículo requiere mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="99a60-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="99a60-199">tooadd una **de nivel de página** filtro para mostrar datos de vehículos, que requieren mantenimiento:</span><span class="sxs-lookup"><span data-stu-id="99a60-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="99a60-200">Hola arrastre **"MaintenanceLabel"** campo **filtros de nivel de página**.</span><span class="sxs-lookup"><span data-stu-id="99a60-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="99a60-201">![Automóviles conectados - Filtros de nivel de página](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="99a60-202">Haga clic en el menú **Filtrado básico** que se encuentra en la parte inferior del filtro de nivel de página MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="99a60-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="99a60-203">![Automóviles conectados - Filtrado básico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="99a60-204">Establezca su valor de filtro demasiado**"1"**  </span><span class="sxs-lookup"><span data-stu-id="99a60-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="99a60-205">![Automóviles conectados - Valor de filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="99a60-206">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-207">Seleccione **Gráfico de columnas agrupadas** en Visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="99a60-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="99a60-208">![Automóviles conectados - Visualización de tarjeta vind](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="99a60-209">![Automóviles conectados - Gráfico de columnas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="99a60-210">Campo de arrastre **modelo** en **eje** área, **Niv** demasiado**valor** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="99a60-211">Después, ordene la visualización por **Recuento de vin**.</span><span class="sxs-lookup"><span data-stu-id="99a60-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="99a60-212">Gráfico de cambio **título** demasiado**"Vehículos que requiere el modelo de mantenimiento"**</span><span class="sxs-lookup"><span data-stu-id="99a60-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="99a60-213">Arrastre los campos **vin** a **Saturación de color**, que se encuentra en la sección **Campos** ![Campos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) de la pestaña **Visualización**.</span><span class="sxs-lookup"><span data-stu-id="99a60-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="99a60-214">![Automóviles conectados - Saturación de color](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="99a60-215">Cambie **Colores de datos** en las visualizaciones de la sección **Formato**.</span><span class="sxs-lookup"><span data-stu-id="99a60-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="99a60-216">Cambie el color mínimo a: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="99a60-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="99a60-217">Cambie el color máximo a: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="99a60-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="99a60-218">![Automóviles conectados - Cambios de color](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="99a60-219">![Automóviles conectados - Nuevos colores de visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="99a60-220">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-221">Seleccione **Gráfico de columnas agrupadas** en Visualizaciones, arrastre el campo **vin** al área **Valor** y arrastre el campo **city** al área **Eje**.</span><span class="sxs-lookup"><span data-stu-id="99a60-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="99a60-222">Ordene el gráfico por **“Recuento de vin”**.</span><span class="sxs-lookup"><span data-stu-id="99a60-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="99a60-223">Gráfico de cambio **título** demasiado**"Vehículos que requiere el mantenimiento por ciudad"** </span><span class="sxs-lookup"><span data-stu-id="99a60-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="99a60-224">![Automóviles conectados - Vehículos que requieren mantenimiento por ciudad](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="99a60-225">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-226">Seleccione **tarjeta de varias filas** visualización de visualizaciones, arrastre **modelo** y **Niv** en hello **campos** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="99a60-227">![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="99a60-228">Reorganizar todo de visualización de hello, informe final hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="99a60-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="99a60-230">Informes en tiempo real de Hola "Vehículos necesidad de mantenimiento" se configuró correctamente.</span><span class="sxs-lookup"><span data-stu-id="99a60-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="99a60-231">Puede continuar informes en tiempo real de toocreate Hola siguiente o deténgase aquí y configuración de panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="99a60-232">3. Estadísticas de estado de los vehículos</span><span class="sxs-lookup"><span data-stu-id="99a60-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="99a60-233">Haga clic en ![agregar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nuevos informes, cambiar el nombre demasiado**"Las estadísticas de estado de vehículos"**</span><span class="sxs-lookup"><span data-stu-id="99a60-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="99a60-234">Seleccione **medidor** visualización de visualizaciones, a continuación, arrastre hello **velocidad** campo **, valor mínimo, máximo valor** áreas.</span><span class="sxs-lookup"><span data-stu-id="99a60-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="99a60-235">![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="99a60-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="99a60-236">Cambiar la agregación predeterminada de Hola de **velocidad** en **valor área** demasiado**promedio**</span><span class="sxs-lookup"><span data-stu-id="99a60-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="99a60-237">Cambiar la agregación predeterminada de Hola de **velocidad** en **área mínimo** demasiado**mínimo**</span><span class="sxs-lookup"><span data-stu-id="99a60-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="99a60-238">Cambiar la agregación predeterminada de Hola de **velocidad** en **área máximo** demasiado**máximo**</span><span class="sxs-lookup"><span data-stu-id="99a60-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="99a60-240">Cambiar el nombre de hello **medidor título** demasiado**"Promedio de velocidad"**</span><span class="sxs-lookup"><span data-stu-id="99a60-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Automóviles conectados - Medidor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="99a60-242">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="99a60-243">Del mismo modo, agregue un **Indicador** para el **aceite medio del motor**, el **combustible medio** y la **temperatura media del motor**.</span><span class="sxs-lookup"><span data-stu-id="99a60-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="99a60-244">Cambiar agregación predeterminada de Hola de campos de cada medidor según por encima de los pasos descritos en **"Promedio de velocidad"** del medidor.</span><span class="sxs-lookup"><span data-stu-id="99a60-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Automóviles conectados - Medidores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="99a60-246">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="99a60-247">Seleccione **línea y gráfico de columnas agrupadas** de visualizaciones, a continuación, arrastre **City** campo **eje compartido**, arrastre **velocidad**, **campos tirepressure y engineoil** en **valores de columna** área, cambiar su tipo de agregación demasiado**Media**.</span><span class="sxs-lookup"><span data-stu-id="99a60-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="99a60-248">Hola arrastre **engineTemperature** campo **valores de las líneas** área, también cambian el tipo de agregación de hello**promedio**.</span><span class="sxs-lookup"><span data-stu-id="99a60-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Automóviles conectados - Campos de visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="99a60-250">Gráfico de cambio hello **título** demasiado**"Promedio velocidad, tire presión, petróleo de motor y temperatura del motor"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Automóviles conectados - Campos de visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="99a60-252">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="99a60-253">Seleccione **Treemap** visualización de visualizaciones, arrastre hello **modelo** campo hello **grupo** área y arrastre Hola campo  **MaintenanceProbability** en hello **valores** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="99a60-254">Gráfico de cambio hello **título** demasiado**"Que requiere el mantenimiento de modelos de vehículo"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="99a60-256">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="99a60-257">Seleccione **gráfico de barras apiladas 100%** de visualización, arrastre hello **city** campo hello **eje** área y arrastre hello **MaintenanceProbability**, **RecallProbability** campos en hello **valor** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="99a60-259">Haga clic en **formato**, seleccione **colores de datos**, conjunto hello y **MaintenanceProbability** toohello valor de color **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="99a60-260">Hola de cambio **título** de hello gráfico demasiado**"Probabilidad de vehículo mantenimiento y recuerde by City"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="99a60-262">Haga clic en nueva visualización de hello área en blanco tooadd.</span><span class="sxs-lookup"><span data-stu-id="99a60-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="99a60-263">Seleccione **gráfico de áreas** de visualización de visualizaciones, arrastre hello **modelo** campo hello **eje** área y arrastre hello **engineOil, tirepressure, velocidad y MaintenanceProbability** campos en hello **valores** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="99a60-264">Cambiar el tipo de agregación también**"Medio"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-264">Change their aggregation type too**“Average”**.</span></span> 

![Automóviles conectados - Cambiar tipo de agregación](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="99a60-266">Cambiar el título de hello del gráfico de hello demasiado**"Promedio de petróleo motor, probabilidad presión, velocidad y el mantenimiento de neumáticos modelo"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="99a60-268">Haga clic en nueva visualización de hello área en blanco tooadd:</span><span class="sxs-lookup"><span data-stu-id="99a60-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="99a60-269">Seleccione la visualización **Gráfico de dispersión** en Visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="99a60-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="99a60-270">Hola arrastre **modelo** campo hello **detalles** y **leyenda** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="99a60-271">Hola arrastre **combustible** campo hello **eje x** área, cambiar las agregaciones de hello también**Media**.</span><span class="sxs-lookup"><span data-stu-id="99a60-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="99a60-272">Arrastre **engineTemparature** en **área de eje y**, cambiar las agregaciones de hello también**promedio**</span><span class="sxs-lookup"><span data-stu-id="99a60-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="99a60-273">Hola arrastre **Niv** campo hello **tamaño** área.</span><span class="sxs-lookup"><span data-stu-id="99a60-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="99a60-275">Gráfico de cambio hello **título** demasiado**"Medias de combustible y temperatura del motor por modelo"**.</span><span class="sxs-lookup"><span data-stu-id="99a60-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="99a60-277">Hola final será informe tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="99a60-277">hello final report will look like as shown below.</span></span>

![Automóviles conectados - Informe final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="99a60-279">Visualizaciones de PIN de panel en tiempo real de hello informes toohello</span><span class="sxs-lookup"><span data-stu-id="99a60-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="99a60-280">Crear un panel en blanco, haga clic en el icono de hello más tooDashboards siguiente.</span><span class="sxs-lookup"><span data-stu-id="99a60-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="99a60-281">Puede asignarle el nombre "Panel de análisis de telemetría de vehículos".</span><span class="sxs-lookup"><span data-stu-id="99a60-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="99a60-283">Visualización de PIN Hola de Hola por encima del panel de toohello de informes.</span><span class="sxs-lookup"><span data-stu-id="99a60-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="99a60-285">panel de Hello debe ser similar al siguiente cuando todos los Hola se crean tres informes y Hola correspondiente visualizaciones están anclados toohello panel.</span><span class="sxs-lookup"><span data-stu-id="99a60-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="99a60-286">Si no ha creado todos los informes de hello, el panel podría ser diferente.</span><span class="sxs-lookup"><span data-stu-id="99a60-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="99a60-288">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="99a60-288">Congratulations!</span></span> <span data-ttu-id="99a60-289">Ha creado correctamente la API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="99a60-290">A medida que continúa tooexecute CarEventGenerator.exe y RealtimeDashboardApp.exe, debería ver actualizaciones directas en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="99a60-291">Tardará hello toocomplete too15 unos 10 minutos que siga los pasos.</span><span class="sxs-lookup"><span data-stu-id="99a60-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="99a60-292">Configuración del panel de procesamiento por lotes de Power BI</span><span class="sxs-lookup"><span data-stu-id="99a60-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="99a60-293">Se tarda aproximadamente dos horas (de realización correcta de Hola de implementación de hello) de ejecución de toofinish la canalización de procesamiento por lotes de tooend de final de hello y procesar un período de año de datos generados.</span><span class="sxs-lookup"><span data-stu-id="99a60-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="99a60-294">Por lo que espere hello toofinish antes de continuar con los pasos siguientes de Hola de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="99a60-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="99a60-295">**Descargar el archivo del diseñador Hola Power BI**</span><span class="sxs-lookup"><span data-stu-id="99a60-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="99a60-296">Un archivo del Diseñador de Power BI configurado previamente se incluye como parte de la implementación de hello las instrucciones de funcionamiento Manual</span><span class="sxs-lookup"><span data-stu-id="99a60-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="99a60-297">Busque 2.</span><span class="sxs-lookup"><span data-stu-id="99a60-297">Look for 2.</span></span> <span data-ttu-id="99a60-298">Panel de procesamiento por lotes de instalación Power BI puede descargar plantilla de Power BI de hello para el panel de procesamiento por lotes llamado **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="99a60-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="99a60-299">Guarde localmente.</span><span class="sxs-lookup"><span data-stu-id="99a60-299">Save locally</span></span>

<span data-ttu-id="99a60-300">**Configuración de informes de Power BI**</span><span class="sxs-lookup"><span data-stu-id="99a60-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="99a60-301">Archivo del diseñador abra hello '**ConnectedCarsPbiReport.pbix**' con Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="99a60-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="99a60-302">Si ya no tiene, instala Hola Power BI Desktop desde [instalación de Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="99a60-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="99a60-303">Haga clic en hello **editar consultas**.</span><span class="sxs-lookup"><span data-stu-id="99a60-303">Click hello **Edit Queries**.</span></span>

![Edición de la consulta de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="99a60-305">Haga doble clic en hello **origen**.</span><span class="sxs-lookup"><span data-stu-id="99a60-305">Double-click hello **Source**.</span></span>

![Establecimiento de origen de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="99a60-307">Actualizar la cadena de conexión de servidor con hello Azure SQL server que se obtuvo suministrado como parte de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="99a60-308">Buscar en las instrucciones de funcionamiento de hello Manual en</span><span class="sxs-lookup"><span data-stu-id="99a60-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="99a60-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="99a60-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="99a60-310">Servidor: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="99a60-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="99a60-311">Base de datos: connectedcar</span><span class="sxs-lookup"><span data-stu-id="99a60-311">Database: connectedcar</span></span>
    * <span data-ttu-id="99a60-312">Nombre de usuario: username</span><span class="sxs-lookup"><span data-stu-id="99a60-312">Username: username</span></span>
    * <span data-ttu-id="99a60-313">Contraseña: Puede administrar la contraseña de SQL Server desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="99a60-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="99a60-314">Establezca **Base de datos** como *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="99a60-314">Leave **Database** as *connectedcar*.</span></span>

![Establecimiento de la base de datos Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="99a60-316">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="99a60-316">Click **OK**.</span></span>
* <span data-ttu-id="99a60-317">Verá **credencial de Windows** ficha seleccionada de forma predeterminada, también cambian**las credenciales de la base de datos** haciendo clic en **base de datos** ficha a la derecha.</span><span class="sxs-lookup"><span data-stu-id="99a60-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="99a60-318">Proporcionar hello **nombre de usuario** y **contraseña** de la base de datos de SQL Azure que se especificó durante la instalación de su implementación.</span><span class="sxs-lookup"><span data-stu-id="99a60-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Introduzca las credenciales de la base de datos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="99a60-320">Haga clic en **Conectar**</span><span class="sxs-lookup"><span data-stu-id="99a60-320">Click **Connect**</span></span>
* <span data-ttu-id="99a60-321">Repita Hola por encima de los pasos para cada uno de hello tres restantes consultas presentes en el panel derecho y, a continuación, actualice los detalles de conexión de origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="99a60-322">Haga clic en **Cerrar y cargar**.</span><span class="sxs-lookup"><span data-stu-id="99a60-322">Click **Close and Load**.</span></span> <span data-ttu-id="99a60-323">Los conjuntos de datos de archivo de Power BI Desktop son tablas de base de datos de Azure tooSQL conectado.</span><span class="sxs-lookup"><span data-stu-id="99a60-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="99a60-324">**Cierre** el archivo de Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="99a60-324">**Close** Power BI Desktop file.</span></span>

![Cierre Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="99a60-326">Haga clic en **guardar** botón toosave Hola cambiará.</span><span class="sxs-lookup"><span data-stu-id="99a60-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="99a60-327">Ya ha configurado todos los informes de hello correspondiente toohello ruta de procesamiento por lotes de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="99a60-328">Cargar demasiado*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="99a60-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="99a60-329">Navegue toohello portal de web de Power BI en http://powerbi.com e inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99a60-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="99a60-330">Haga clic en **Obtener datos**</span><span class="sxs-lookup"><span data-stu-id="99a60-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="99a60-331">Cargar archivo de Power BI Desktop Hola.</span><span class="sxs-lookup"><span data-stu-id="99a60-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="99a60-332">tooupload, haga clic en **obtener datos -> archivos Get -> archivo Local**</span><span class="sxs-lookup"><span data-stu-id="99a60-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="99a60-333">Navegue toohello **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="99a60-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="99a60-334">Una vez cargado el archivo hello, será tooyour atrás navegar de un área de trabajo de Power BI.</span><span class="sxs-lookup"><span data-stu-id="99a60-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="99a60-335">Se crearán un conjunto de datos, un informe y un panel en blanco.</span><span class="sxs-lookup"><span data-stu-id="99a60-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="99a60-336">Gráficos de PIN tooa nuevo panel denominado **panel de análisis de telemetría de vehículo** en **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="99a60-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="99a60-337">Haga clic en panel en blanco Hola creado anteriormente y, a continuación, navegue toohello **informes** sección, haga clic Hola recién cargado el informe.</span><span class="sxs-lookup"><span data-stu-id="99a60-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Telemetría de vehículos Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="99a60-339">**Tenga en cuenta Hola informe tiene seis páginas:**</span><span class="sxs-lookup"><span data-stu-id="99a60-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="99a60-340">Página 1: Densidad de vehículos</span><span class="sxs-lookup"><span data-stu-id="99a60-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="99a60-341">Página 2: Estado de vehículos en tiempo real</span><span class="sxs-lookup"><span data-stu-id="99a60-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="99a60-342">Página 3: Vehículos conducidos de forma agresiva</span><span class="sxs-lookup"><span data-stu-id="99a60-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="99a60-343">Página 4: Vehículos retirados</span><span class="sxs-lookup"><span data-stu-id="99a60-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="99a60-344">Página 5: Vehículos conducidos con un consumo eficiente</span><span class="sxs-lookup"><span data-stu-id="99a60-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="99a60-345">Página 6: Logotipo de Contoso</span><span class="sxs-lookup"><span data-stu-id="99a60-345">Page 6: Contoso Logo</span></span>  

![Automóviles conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="99a60-347">**Desde la página 3**, anclar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="99a60-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="99a60-348">Recuento de vin</span><span class="sxs-lookup"><span data-stu-id="99a60-348">Count of VIN</span></span>  
   ![Automóviles conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="99a60-350">Vehículos que se han conducido de forma agresiva por modelo: gráfico de cascada </span><span class="sxs-lookup"><span data-stu-id="99a60-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="99a60-352">**Desde la página 5**, anclar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="99a60-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="99a60-353">Recuento de vin</span><span class="sxs-lookup"><span data-stu-id="99a60-353">Count of vin</span></span>    
   ![Telemetría del vehículo - Anclar gráficos 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="99a60-355">Vehículos con ahorro de combustible por modelo: gráfico de columnas agrupadas </span><span class="sxs-lookup"><span data-stu-id="99a60-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="99a60-357">**En la página 4**, anclar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="99a60-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="99a60-358">Recuento de vin</span><span class="sxs-lookup"><span data-stu-id="99a60-358">Count of vin</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="99a60-360">Vehículos retirados por ciudad y modelo: gráfico de rectángulos </span><span class="sxs-lookup"><span data-stu-id="99a60-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="99a60-362">**Página 6**, anclar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="99a60-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="99a60-363">Logotipo de Contoso Motors</span><span class="sxs-lookup"><span data-stu-id="99a60-363">Contoso Motors logo</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="99a60-365">**Organizar Hola panel**</span><span class="sxs-lookup"><span data-stu-id="99a60-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="99a60-366">Vaya a Panel de toohello</span><span class="sxs-lookup"><span data-stu-id="99a60-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="99a60-367">Mantenga el mouse sobre cada gráfico y cambie su nombre en función de nomenclatura de hello proporcionadas en hello panel completa de las siguientes imágenes.</span><span class="sxs-lookup"><span data-stu-id="99a60-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="99a60-368">Mover gráficos Hola alrededor toolook como Hola panel siguiente.</span><span class="sxs-lookup"><span data-stu-id="99a60-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Telemetría del vehículo - Organizar panel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Telemetría de vehículos Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="99a60-371">Si ha creado todos los informes de hello como se ha mencionado en este documento, hello final panel completado debería parecerse Hola figura siguiente.</span><span class="sxs-lookup"><span data-stu-id="99a60-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Telemetría del vehículo - Organizar panel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="99a60-373">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="99a60-373">Congratulations!</span></span> <span data-ttu-id="99a60-374">Se han creado correctamente los informes de Hola y Hola toogain de panel en tiempo real, predicción y transformación de la visión de lote en el estado de vehículo y dirigir.</span><span class="sxs-lookup"><span data-stu-id="99a60-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
