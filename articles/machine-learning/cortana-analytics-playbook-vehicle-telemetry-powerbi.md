---
title: "Panel de Power BI del estado de vehículo y los hábitos de conducción - Azure | Microsoft Docs"
description: "Aproveche las posibilidades de Cortana Intelligence para obtener información en tiempo real y predictiva del estado de los vehículos y los hábitos de conducción."
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="38cb5-103">Instrucciones de configuración del panel de Power BI para la plantilla de la solución Análisis de telemetría de vehículos</span><span class="sxs-lookup"><span data-stu-id="38cb5-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="38cb5-104">Este **menú** está relacionado con los capítulos de este cuaderno de estrategias.</span><span class="sxs-lookup"><span data-stu-id="38cb5-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="38cb5-105">La solución de análisis de telemetría de vehículos muestra cómo los concesionarios y los fabricantes de automóviles, así como las compañías de seguros, pueden aprovechar las posibilidades de Cortana Intelligence para obtener información predictiva y en tiempo real sobre el estado del vehículo y los hábitos de conducción con el objetivo de impulsar mejoras en el área de la experiencia del cliente, el I+D y las campañas de marketing.</span><span class="sxs-lookup"><span data-stu-id="38cb5-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="38cb5-106">Este documento contiene instrucciones paso a paso sobre cómo configurar el panel y los informes de Power BI una vez que la solución se implementa en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="38cb5-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="38cb5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38cb5-107">Prerequisites</span></span>
1. <span data-ttu-id="38cb5-108">Implementar las soluciones de [análisis de telemetría](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)</span><span class="sxs-lookup"><span data-stu-id="38cb5-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="38cb5-109">Instalar Microsoft Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="38cb5-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="38cb5-110">Una [suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38cb5-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="38cb5-111">Si no tiene una suscripción de Azure, comience con una suscripción gratis de Azure.</span><span class="sxs-lookup"><span data-stu-id="38cb5-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="38cb5-112">Cuenta de Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="38cb5-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="38cb5-113">Componentes de Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="38cb5-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="38cb5-114">Como parte de la plantilla de la solución de análisis de telemetría de vehículo, se implementan los siguientes servicios de Cortana Intelligence en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="38cb5-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="38cb5-115">**Centro de eventos** para la introducción de millones de eventos de telemetría del vehículo en Azure.</span><span class="sxs-lookup"><span data-stu-id="38cb5-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="38cb5-116">**Análisis de transmisiones** para obtener información en tiempo real sobre el estado del vehículo y conserva los datos en el almacenamiento a largo plazo para análisis de lotes más completo.</span><span class="sxs-lookup"><span data-stu-id="38cb5-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="38cb5-117">**Aprendizaje automático** para la detección de anomalías en tiempo real y el procesamiento por lotes para obtener información predictiva.</span><span class="sxs-lookup"><span data-stu-id="38cb5-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="38cb5-118">**HDInsight** se aprovecha para transformar datos a escala.</span><span class="sxs-lookup"><span data-stu-id="38cb5-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="38cb5-119">**Factoría de datos** controla la orquestación, la programación, la administración de recursos y la supervisión de la canalización del procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="38cb5-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="38cb5-120">**Power BI** ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="38cb5-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="38cb5-121">La solución usa dos orígenes de datos diferentes: **señales simuladas de vehículos y conjunto de datos de diagnóstico** y el **catálogo de vehículos**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="38cb5-122">Se incluye un simulador telemático del vehículo como parte de esta solución.</span><span class="sxs-lookup"><span data-stu-id="38cb5-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="38cb5-123">Este simulador emite información de diagnóstico y señales correspondientes al estado del vehículo y al patrón de conducción en un momento dado en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="38cb5-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="38cb5-124">El catálogo de vehículo es un conjunto de datos de referencia que contiene una asignación de número de identificación del vehículo (VIN) a modelo.</span><span class="sxs-lookup"><span data-stu-id="38cb5-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="38cb5-125">Preparación de panel de Power BI</span><span class="sxs-lookup"><span data-stu-id="38cb5-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="38cb5-126">Configuración del panel de Power BI en tiempo real</span><span class="sxs-lookup"><span data-stu-id="38cb5-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="38cb5-127">**Inicio de la aplicación de panel en tiempo real** Una vez completada la implementación, debe seguir las instrucciones de funcionamiento manual</span><span class="sxs-lookup"><span data-stu-id="38cb5-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="38cb5-128">Descargue la aplicación de panel en tiempo real RealtimeDashboardApp.zip y descomprímala.</span><span class="sxs-lookup"><span data-stu-id="38cb5-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="38cb5-129">En la carpeta descomprimida, abra el archivo de configuración de la aplicación 'RealtimeDashboardApp.exe.config,' reemplace appSettings para las conexiones de servicio de Eventhub, Blob Storage y ML con los valores en las instrucciones de funcionamiento manual y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="38cb5-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="38cb5-130">Ejecute la aplicación RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="38cb5-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="38cb5-131">Aparecerá una ventana de inicio de sesión. Proporcione sus credenciales de Power BI válidas y haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="38cb5-132">A continuación, la aplicación comenzará a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="38cb5-132">Then the app will start to run.</span></span>

   ![Inicio de sesión en Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Permisos de panel de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="38cb5-135">Inicie sesión en el sitio web de Power BI y cree un panel en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="38cb5-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="38cb5-136">Ahora, está listo para configurar el panel de Power BI con visualizaciones enriquecidas para obtener información predictiva y en tiempo real sobre el estado del vehículo y los hábitos de conducción.</span><span class="sxs-lookup"><span data-stu-id="38cb5-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="38cb5-137">Se tarda entre 45 minutos y una hora en crear todos los informes y configurar el panel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="38cb5-138">Configuración de informes de Power BI</span><span class="sxs-lookup"><span data-stu-id="38cb5-138">Configure Power BI reports</span></span>
<span data-ttu-id="38cb5-139">Los informes y el panel en tiempo real tardan aproximadamente entre 30 y 45 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="38cb5-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="38cb5-140">Vaya a [http://powerbi.com](http://powerbi.com) e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="38cb5-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Inicio de sesión en Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="38cb5-142">Se genera un nuevo conjunto de datos en Power BI.</span><span class="sxs-lookup"><span data-stu-id="38cb5-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="38cb5-143">Haga clic en el conjunto de datos **ConnectedCarsRealtime** .</span><span class="sxs-lookup"><span data-stu-id="38cb5-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Seleccione conjunto de datos en tiempo real de automóviles conectados.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="38cb5-145">Guarde el informe en blanco mediante la combinación de teclas **Ctrl + S**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-145">Save the blank report using **Ctrl + s**.</span></span>

![Guardar el informe en blanco](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="38cb5-147">Proporcione el nombre del informe *Análisis de telemetría del vehículo en tiempo real - Informes*.</span><span class="sxs-lookup"><span data-stu-id="38cb5-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Proporcione el nombre del informe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="38cb5-149">Informes en tiempo real</span><span class="sxs-lookup"><span data-stu-id="38cb5-149">Real-time reports</span></span>
<span data-ttu-id="38cb5-150">Hay tres informes en tiempo real en esta solución:</span><span class="sxs-lookup"><span data-stu-id="38cb5-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="38cb5-151">Vehículos en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="38cb5-151">Vehicles in operation</span></span>
2. <span data-ttu-id="38cb5-152">Vehículos que requieren mantenimiento</span><span class="sxs-lookup"><span data-stu-id="38cb5-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="38cb5-153">Estadísticas de estado de los vehículos</span><span class="sxs-lookup"><span data-stu-id="38cb5-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="38cb5-154">Puede elegir configurar los tres informes en tiempo real o parar después de una fase y continuar con la siguiente sección de configuración de los informes por lotes.</span><span class="sxs-lookup"><span data-stu-id="38cb5-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="38cb5-155">Se recomienda crear los tres informes para visualizar la información completa de la ruta en tiempo real de la solución.</span><span class="sxs-lookup"><span data-stu-id="38cb5-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="38cb5-156">1. Vehículos en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="38cb5-156">1. Vehicles in operation</span></span>
<span data-ttu-id="38cb5-157">Haga doble clic en **Página 1** y cambie el nombre de la página a “Vehículos en funcionamiento”.</span><span class="sxs-lookup"><span data-stu-id="38cb5-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="38cb5-158">![Automóviles conectados: Vehículos en funcionamiento](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="38cb5-159">Seleccione el campo **vin** en **Campos** y elija el tipo de visualización como **“Tarjeta”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="38cb5-160">Se crea la visualización de tarjeta como se muestra en la ilustración.</span><span class="sxs-lookup"><span data-stu-id="38cb5-160">Card visualization is created as shown in figure.</span></span>  
    ![Automóviles conectados - Seleccionar vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="38cb5-162">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-163">Seleccione **city** y **vin** en los campos.</span><span class="sxs-lookup"><span data-stu-id="38cb5-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="38cb5-164">Cambie la visualización a **"Mapa"**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="38cb5-165">Arrastre **vin** al área de valores.</span><span class="sxs-lookup"><span data-stu-id="38cb5-165">Drag **vin** in values area.</span></span> <span data-ttu-id="38cb5-166">Arrastre **city** desde los campos hasta el área **Leyenda**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="38cb5-167">![Automóviles conectados: Visualización de tarjeta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="38cb5-168">Seleccione la sección **Formato** en **Visualizaciones**, haga clic en **Título** y cambie el **texto** a **“Vehículos en funcionamiento por ciudad”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="38cb5-169">![Automóviles conectados: Vehículos en funcionamiento por ciudad](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="38cb5-170">La visualización final tiene el aspecto que se muestra en la ilustración.</span><span class="sxs-lookup"><span data-stu-id="38cb5-170">Final visualization looks as shown in figure.</span></span>    
    ![Automóviles conectados - Visualización final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="38cb5-172">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-173">Seleccione **city** y **vin**, cambie el tipo de visualización a **Gráfico de columnas agrupadas**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="38cb5-174">Asegúrese de que el campo **city** esté en el área **Eje** y **vin** en el área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="38cb5-175">Ordene el gráfico por **“Recuento de vin”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="38cb5-176">![Automóviles conectados: Recuento de vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="38cb5-177">Cambie el **Título** del gráfico a **“Vehículos en funcionamiento por ciudad”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="38cb5-178">Haga clic en la sección **Formato** y, después, seleccione **Colores de datos**. Haga clic en **“Activar”** para **Mostrar todo**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="38cb5-179">![Automóviles conectados: Mostrar todos los colores de datos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="38cb5-180">Cambie el color de cada ciudad haciendo clic en el icono de color.</span><span class="sxs-lookup"><span data-stu-id="38cb5-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Automóviles conectados - Cambiar colores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="38cb5-182">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-183">Seleccione la visualización **Gráfico de columnas agrupadas** en Visualizaciones, arrastre el campo **city** al área **Eje**, el campo **Model** al área **Leyenda** y el campo **vin** al área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="38cb5-184">![Automóviles conectados: Gráfico de columnas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="38cb5-185">![Automóviles conectados: Representación](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="38cb5-186">Reorganice toda la visualización de esta página como se muestra en la ilustración.</span><span class="sxs-lookup"><span data-stu-id="38cb5-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Automóviles conectados - Visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="38cb5-188">Ha configurado correctamente el informe en tiempo real de "Vehículos en funcionamiento".</span><span class="sxs-lookup"><span data-stu-id="38cb5-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="38cb5-189">Puede continuar y crear el siguiente informe en tiempo real o detenerse aquí y configurar el panel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="38cb5-190">2. Vehículos que requieren mantenimiento</span><span class="sxs-lookup"><span data-stu-id="38cb5-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="38cb5-191">Haga clic en ![Agregar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) para agregar un nuevo informe y cambie su nombre a **"Vehículos que requieren mantenimiento"**</span><span class="sxs-lookup"><span data-stu-id="38cb5-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Automóviles conectados - Vehículos que requieren mantenimiento](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="38cb5-193">Seleccione el campo **vin** y cambie el tipo de visualización a **Tarjeta**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="38cb5-194">![Automóviles conectados: Visualización de tarjeta vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="38cb5-195">En el conjunto de datos, tenemos un campo llamado "MaintenanceLabel".</span><span class="sxs-lookup"><span data-stu-id="38cb5-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="38cb5-196">Este campo puede tener un valor de "0" o "1".</span><span class="sxs-lookup"><span data-stu-id="38cb5-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="38cb5-197">Lo establece el modelo de aprendizaje automático de Azure aprovisionado como parte de la solución y se integra con la ruta en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="38cb5-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="38cb5-198">El valor "1" indica que un vehículo requiere mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="38cb5-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="38cb5-199">Iremos agregando filtros de **nivel de página** para mostrar datos de vehículos que requieren mantenimiento:</span><span class="sxs-lookup"><span data-stu-id="38cb5-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="38cb5-200">Arrastre el campo **“MaintenanceLabel”** a **Filtros de nivel de página**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="38cb5-201">![Automóviles conectados - Filtros de nivel de página](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="38cb5-202">Haga clic en el menú **Filtrado básico** que se encuentra en la parte inferior del filtro de nivel de página MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="38cb5-203">![Automóviles conectados - Filtrado básico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="38cb5-204">Establezca su valor de filtro en **“1”**  .</span><span class="sxs-lookup"><span data-stu-id="38cb5-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="38cb5-205">![Automóviles conectados - Valor de filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="38cb5-206">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-207">Seleccione **Gráfico de columnas agrupadas** en Visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="38cb5-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="38cb5-208">![Automóviles conectados - Visualización de tarjeta vind](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="38cb5-209">![Automóviles conectados - Gráfico de columnas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="38cb5-210">Arrastre el campo **Model** al área **Eje** y el campo **vin** al área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="38cb5-211">Después, ordene la visualización por **Recuento de vin**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="38cb5-212">Cambie el **Título** del gráfico a **“Vehículos que necesitan mantenimiento por modelo”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="38cb5-213">Arrastre los campos **vin** a **Saturación de color**, que se encuentra en la sección **Campos** ![Campos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) de la pestaña **Visualización**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="38cb5-214">![Automóviles conectados - Saturación de color](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="38cb5-215">Cambie **Colores de datos** en las visualizaciones de la sección **Formato**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="38cb5-216">Cambie el color mínimo a: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="38cb5-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="38cb5-217">Cambie el color máximo a: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="38cb5-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="38cb5-218">![Automóviles conectados - Cambios de color](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="38cb5-219">![Automóviles conectados - Nuevos colores de visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="38cb5-220">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-221">Seleccione **Gráfico de columnas agrupadas** en Visualizaciones, arrastre el campo **vin** al área **Valor** y arrastre el campo **city** al área **Eje**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="38cb5-222">Ordene el gráfico por **“Recuento de vin”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="38cb5-223">Cambie el **Título** del gráfico a **“Vehículos que necesitan mantenimiento por ciudad”** .</span><span class="sxs-lookup"><span data-stu-id="38cb5-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="38cb5-224">![Automóviles conectados - Vehículos que requieren mantenimiento por ciudad](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="38cb5-225">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-226">Seleccione la visualización **Tarjeta de varias filas** en Visualizaciones y arrastre los campos **Model** y **vin** al área **Campos**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="38cb5-227">![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="38cb5-228">Al reorganizar todos los datos de la visualización, el informe final tiene el aspecto siguiente: </span><span class="sxs-lookup"><span data-stu-id="38cb5-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="38cb5-230">Ha configurado correctamente el informe en tiempo real "Vehículos que requieren mantenimiento".</span><span class="sxs-lookup"><span data-stu-id="38cb5-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="38cb5-231">Puede continuar y crear el siguiente informe en tiempo real o detenerse aquí y configurar el panel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="38cb5-232">3. Estadísticas de estado de los vehículos</span><span class="sxs-lookup"><span data-stu-id="38cb5-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="38cb5-233">Haga clic en ![Agregar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) para agregar el nuevo informe y cambie su nombre a **"Estadísticas de estado de los vehículos"**</span><span class="sxs-lookup"><span data-stu-id="38cb5-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="38cb5-234">Seleccione la visualización **Indicador** en Visualizaciones y, después, arrastre el campo **speed** a las áreas **Valor, Valor mínimo y Valor máximo**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="38cb5-235">![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="38cb5-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="38cb5-236">Cambie la agregación predeterminada de **speed** en el área **Valor** a **Media**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="38cb5-237">Cambie la agregación predeterminada de **speed** en el área **Valor mínimo** a **Mínimo**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="38cb5-238">Cambie la agregación predeterminada de **speed** en el área **Valor máximo** a **Máximo**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="38cb5-240">Cambie el nombre de **Título del indicador** a **“Velocidad media”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Automóviles conectados - Medidor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="38cb5-242">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="38cb5-243">Del mismo modo, agregue un **Indicador** para el **aceite medio del motor**, el **combustible medio** y la **temperatura media del motor**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="38cb5-244">Cambie la agregación predeterminada de los campos de cada indicador según los pasos anteriores del indicador de **"Velocidad media"** .</span><span class="sxs-lookup"><span data-stu-id="38cb5-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Automóviles conectados - Medidores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="38cb5-246">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="38cb5-247">Seleccione **Gráfico de columnas agrupadas y de líneas** en Visualizaciones y, después, arrastre el campo **city** a **Eje compartido** y los campos **speed**, **tirepressure y engineoil** al área **Valores de columna**. Después, cambie su tipo de agregación a **Media**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="38cb5-248">Arrastre el campo **engineTemperature** al área **Valores de línea** y cambie el tipo de agregación a **Media**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Automóviles conectados - Campos de visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="38cb5-250">Cambie el **Título** del gráfico a **“Promedio de velocidad media, presión de los neumáticos, aceite del motor y temperatura del motor”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Automóviles conectados - Campos de visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="38cb5-252">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="38cb5-253">Seleccione la visualización **Gráfico de rectángulos** en Visualizaciones, arrastre el campo **Model** al área **Grupo** y el campo **MaintenanceProbability** al área **Valores**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="38cb5-254">Cambie el **Título** del gráfico a **“Modelos de vehículo que necesitan mantenimiento”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="38cb5-256">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="38cb5-257">Seleccione la visualización **Gráfico de barras 100 % apiladas**, arrastre el campo **city** al área **Eje** y los campos **MaintenanceProbability** y **RecallProbability** al área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="38cb5-259">Haga clic en **Formato**, seleccione **Colores de datos** y establezca el color de **MaintenanceProbability** en el valor **“F2C80F”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="38cb5-260">Cambie el **Título** del gráfico a **“Probabilidad de mantenimiento del vehículo y retirada por ciudad”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="38cb5-262">Haga clic en el área en blanco para agregar una nueva visualización.</span><span class="sxs-lookup"><span data-stu-id="38cb5-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="38cb5-263">Seleccione la visualización **Gráfico de áreas** en Visualizaciones, arrastre el campo **Model** al área **Eje** y los campos **engineOil, tirepressure, speed y MaintenanceProbability** al área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="38cb5-264">Cambie el tipo de agregación a **"Promedio"**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-264">Change their aggregation type to **“Average”**.</span></span> 

![Automóviles conectados - Cambiar tipo de agregación](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="38cb5-266">Cambie el título del gráfico a **"Promedio de aceite del motor, presión de los neumáticos, velocidad y probabilidad de mantenimiento por modelo"**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="38cb5-268">Haga clic en el área en blanco para agregar una nueva visualización:</span><span class="sxs-lookup"><span data-stu-id="38cb5-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="38cb5-269">Seleccione la visualización **Gráfico de dispersión** en Visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="38cb5-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="38cb5-270">Arrastre el campo **Model** al área **Detalles** y **Leyenda**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="38cb5-271">Arrastre el campo **fuel** al área **Eje X** y cambie la agregación a **Media**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="38cb5-272">Arrastre el campo **engineTemperature** al área **Eje Y** y cambie la agregación a **Media**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="38cb5-273">Arrastre el campo **vin** al área **Tamaño**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-273">Drag the **vin** field into the **Size** area.</span></span>

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="38cb5-275">Cambie el **Título** del gráfico a **“Medias de combustible y temperatura del motor por modelo”**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="38cb5-277">El informe final será similar al mostrado a continuación.</span><span class="sxs-lookup"><span data-stu-id="38cb5-277">The final report will look like as shown below.</span></span>

![Automóviles conectados - Informe final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="38cb5-279">Anclaje de las visualizaciones desde los informes al panel en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="38cb5-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="38cb5-280">Cree un panel en blanco haciendo clic en el icono del signo más junto a Paneles.</span><span class="sxs-lookup"><span data-stu-id="38cb5-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="38cb5-281">Puede asignarle el nombre "Panel de análisis de telemetría de vehículos".</span><span class="sxs-lookup"><span data-stu-id="38cb5-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="38cb5-283">Ancle la visualización de los informes anteriores al panel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="38cb5-285">Cuando los tres informes se crean y las visualizaciones correspondientes se anclan al panel, el panel debe verse como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="38cb5-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="38cb5-286">Puede parecer diferente si no ha creado todos los informes.</span><span class="sxs-lookup"><span data-stu-id="38cb5-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="38cb5-288">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="38cb5-288">Congratulations!</span></span> <span data-ttu-id="38cb5-289">Ha creado correctamente el panel en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="38cb5-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="38cb5-290">Mientras sigue ejecutando CarEventGenerator.exe y RealtimeDashboardApp.exe, verá actualizaciones en directo en el panel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="38cb5-291">En unos 10 o 15 minutos se completarán los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="38cb5-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="38cb5-292">Configuración del panel de procesamiento por lotes de Power BI</span><span class="sxs-lookup"><span data-stu-id="38cb5-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="38cb5-293">La canalización del procesamiento por lotes de un extremo a otro tarda unas dos horas en ejecutarse (a partir de la finalización correcta de la implementación) y en procesar un año de datos generados.</span><span class="sxs-lookup"><span data-stu-id="38cb5-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="38cb5-294">Por tanto, espere a que el procesamiento finalice antes de continuar con los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="38cb5-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="38cb5-295">**Descarga del archivo de Power BI Designer**</span><span class="sxs-lookup"><span data-stu-id="38cb5-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="38cb5-296">Se incluye un archivo de Power BI Designer configurado previamente como parte de las instrucciones de funcionamiento manual.</span><span class="sxs-lookup"><span data-stu-id="38cb5-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="38cb5-297">Busque 2.</span><span class="sxs-lookup"><span data-stu-id="38cb5-297">Look for 2.</span></span> <span data-ttu-id="38cb5-298">Configuración del panel de procesamiento por lotes de PowerBI Puede descargar la plantilla de PowerBI para el panel de procesamiento por lotes aquí denominada **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="38cb5-299">Guarde localmente.</span><span class="sxs-lookup"><span data-stu-id="38cb5-299">Save locally</span></span>

<span data-ttu-id="38cb5-300">**Configuración de informes de Power BI**</span><span class="sxs-lookup"><span data-stu-id="38cb5-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="38cb5-301">Abra el archivo del diseñador '**ConnectedCarsPbiReport.pbix**' con Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="38cb5-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="38cb5-302">Si no lo ha hecho ya, instale Power BI Desktop desde la [instalación de Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="38cb5-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="38cb5-303">Haga clic en **Editar consultas**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-303">Click the **Edit Queries**.</span></span>

![Edición de la consulta de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="38cb5-305">Haga doble clic en el **Origen**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-305">Double-click the **Source**.</span></span>

![Establecimiento de origen de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="38cb5-307">Actualice la cadena de conexión de servidor con el servidor SQL de Azure que se ha aprovisionado como parte de la implementación.</span><span class="sxs-lookup"><span data-stu-id="38cb5-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="38cb5-308">Busque en las instrucciones de funcionamiento manual en:</span><span class="sxs-lookup"><span data-stu-id="38cb5-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="38cb5-309">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="38cb5-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="38cb5-310">Servidor: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="38cb5-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="38cb5-311">Base de datos: connectedcar</span><span class="sxs-lookup"><span data-stu-id="38cb5-311">Database: connectedcar</span></span>
    * <span data-ttu-id="38cb5-312">Nombre de usuario: username</span><span class="sxs-lookup"><span data-stu-id="38cb5-312">Username: username</span></span>
    * <span data-ttu-id="38cb5-313">Contraseña: Puede administrar la contraseña de SQL Server desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="38cb5-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="38cb5-314">Establezca **Base de datos** como *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="38cb5-314">Leave **Database** as *connectedcar*.</span></span>

![Establecimiento de la base de datos Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="38cb5-316">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-316">Click **OK**.</span></span>
* <span data-ttu-id="38cb5-317">Verá la pestaña **Credenciales de Windows** seleccionada de forma predeterminada, cámbiela a **Credenciales de base de datos** (para hacerlo, haga clic en la pestaña **Base de datos** a la derecha).</span><span class="sxs-lookup"><span data-stu-id="38cb5-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="38cb5-318">Especifique los valores de **Nombre de usuario** y **Contraseña** de la Azure SQL Database que ha especificado durante la instalación de su implementación.</span><span class="sxs-lookup"><span data-stu-id="38cb5-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Introduzca las credenciales de la base de datos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="38cb5-320">Haga clic en **Conectar**</span><span class="sxs-lookup"><span data-stu-id="38cb5-320">Click **Connect**</span></span>
* <span data-ttu-id="38cb5-321">Repita los pasos anteriores para cada una de las 3 consultas restantes del panel derecho y, después, actualice los detalles de conexión del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="38cb5-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="38cb5-322">Haga clic en **Cerrar y cargar**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-322">Click **Close and Load**.</span></span> <span data-ttu-id="38cb5-323">Los conjuntos de datos de archivos de Power BI Desktop se conectan a tablas de Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="38cb5-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="38cb5-324">**Cierre** el archivo de Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="38cb5-324">**Close** Power BI Desktop file.</span></span>

![Cierre Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="38cb5-326">Haga clic en el botón **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="38cb5-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="38cb5-327">Ahora, ha configurado todos los informes correspondientes a la ruta de procesamiento por lotes de la solución.</span><span class="sxs-lookup"><span data-stu-id="38cb5-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="38cb5-328">Carga en *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="38cb5-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="38cb5-329">Navegue hasta el portal web de Power BI en http://powerbi.com e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="38cb5-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="38cb5-330">Haga clic en **Obtener datos**</span><span class="sxs-lookup"><span data-stu-id="38cb5-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="38cb5-331">Cargue el archivo de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="38cb5-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="38cb5-332">Para cargarlo, haga clic en **Obtener datos -> Archivos Get -> Archivo local**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="38cb5-333">Navegue hasta **"**ConnectedCarsPbiReport.pbix**"**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="38cb5-334">Una vez cargado el archivo, volverá al espacio de trabajo de Power BI.</span><span class="sxs-lookup"><span data-stu-id="38cb5-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="38cb5-335">Se crearán un conjunto de datos, un informe y un panel en blanco.</span><span class="sxs-lookup"><span data-stu-id="38cb5-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="38cb5-336">Ancle los gráficos al panel nuevo denominado **Panel de análisis de telemetría de vehículos** en **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="38cb5-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="38cb5-337">Haga clic en el panel en blanco creado anteriormente y luego vaya a la sección **Informes** y haga clic en el informe recién cargado.</span><span class="sxs-lookup"><span data-stu-id="38cb5-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Telemetría de vehículos Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="38cb5-339">**Tenga en cuenta que el informe tiene seis páginas:**</span><span class="sxs-lookup"><span data-stu-id="38cb5-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="38cb5-340">Página 1: Densidad de vehículos</span><span class="sxs-lookup"><span data-stu-id="38cb5-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="38cb5-341">Página 2: Estado de vehículos en tiempo real</span><span class="sxs-lookup"><span data-stu-id="38cb5-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="38cb5-342">Página 3: Vehículos conducidos de forma agresiva</span><span class="sxs-lookup"><span data-stu-id="38cb5-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="38cb5-343">Página 4: Vehículos retirados</span><span class="sxs-lookup"><span data-stu-id="38cb5-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="38cb5-344">Página 5: Vehículos conducidos con un consumo eficiente</span><span class="sxs-lookup"><span data-stu-id="38cb5-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="38cb5-345">Página 6: Logotipo de Contoso</span><span class="sxs-lookup"><span data-stu-id="38cb5-345">Page 6: Contoso Logo</span></span>  

![Automóviles conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="38cb5-347">**En la página 3**, ancle lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="38cb5-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="38cb5-348">Recuento de vin</span><span class="sxs-lookup"><span data-stu-id="38cb5-348">Count of VIN</span></span>  
   ![Automóviles conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="38cb5-350">Vehículos que se han conducido de forma agresiva por modelo: gráfico de cascada </span><span class="sxs-lookup"><span data-stu-id="38cb5-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="38cb5-352">**En la página 5**, ancle lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="38cb5-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="38cb5-353">Recuento de vin</span><span class="sxs-lookup"><span data-stu-id="38cb5-353">Count of vin</span></span>    
   ![Telemetría del vehículo - Anclar gráficos 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="38cb5-355">Vehículos con ahorro de combustible por modelo: gráfico de columnas agrupadas </span><span class="sxs-lookup"><span data-stu-id="38cb5-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="38cb5-357">**En la página 4**, ancle lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="38cb5-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="38cb5-358">Recuento de vin</span><span class="sxs-lookup"><span data-stu-id="38cb5-358">Count of vin</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="38cb5-360">Vehículos retirados por ciudad y modelo: gráfico de rectángulos </span><span class="sxs-lookup"><span data-stu-id="38cb5-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="38cb5-362">**En la página 6**, ancle lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="38cb5-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="38cb5-363">Logotipo de Contoso Motors</span><span class="sxs-lookup"><span data-stu-id="38cb5-363">Contoso Motors logo</span></span>  
   ![Telemetría del vehículo - Anclar gráficos 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="38cb5-365">**Organización del panel**</span><span class="sxs-lookup"><span data-stu-id="38cb5-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="38cb5-366">Vaya al panel.</span><span class="sxs-lookup"><span data-stu-id="38cb5-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="38cb5-367">Mantenga el puntero sobre cada gráfico y cambie su nombre en función de la nomenclatura proporcionada en la siguiente imagen de panel completo.</span><span class="sxs-lookup"><span data-stu-id="38cb5-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="38cb5-368">Asimismo, mueva los gráficos de un lado a otro hasta conseguir un aspecto del panel similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="38cb5-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Telemetría del vehículo - Organizar panel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Telemetría de vehículos Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="38cb5-371">Si ha creado todos los informes como se ha mencionado en este documento, el panel completado final debe parecerse al de la siguiente ilustración.</span><span class="sxs-lookup"><span data-stu-id="38cb5-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Telemetría del vehículo - Organizar panel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="38cb5-373">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="38cb5-373">Congratulations!</span></span> <span data-ttu-id="38cb5-374">Ha creado correctamente los informes y el panel para obtener información predictiva y por lotes en tiempo real sobre los hábitos de mantenimiento y conducción.</span><span class="sxs-lookup"><span data-stu-id="38cb5-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
