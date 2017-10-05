---
title: "Visualización de información en tiempo real de los datos del sensor desde Azure IoT Hub – Power BI | Microsoft Docs"
description: "Use Power BI para visualizar datos de temperatura y humedad que se recopilan desde el sensor y se le envían a Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualización de datos en tiempo real, visualización de datos en directo, visualización de datos de sensor"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="d29dc-104">Visualización de datos del sensor en tiempo real desde Azure IoT Hub mediante Power BI</span><span class="sxs-lookup"><span data-stu-id="d29dc-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="d29dc-106">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="d29dc-106">What you learn</span></span>

<span data-ttu-id="d29dc-107">Aprenderá a visualizar los datos del sensor en tiempo real que recibe el centro de Azure IoT recibe mediante Power BI.</span><span class="sxs-lookup"><span data-stu-id="d29dc-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="d29dc-108">Si desea intentar visualizar los datos en IoT Hub con Web Apps, consulte [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md) (Uso de Azure Web Apps para visualizar datos del sensor en tiempo real desde Azure IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="d29dc-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="d29dc-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="d29dc-109">What you do</span></span>

- <span data-ttu-id="d29dc-110">Prepare el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="d29dc-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="d29dc-111">Cree, configure y ejecute un trabajo de Stream Analytics para la transferencia de datos desde su IoT Hub a su cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="d29dc-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="d29dc-112">Cree y publique un informe de Power BI para visualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="d29dc-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d29dc-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="d29dc-113">What you need</span></span>

- <span data-ttu-id="d29dc-114">Tutorial [Instalación de su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde se abordan los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="d29dc-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="d29dc-115">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d29dc-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="d29dc-116">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="d29dc-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="d29dc-117">Una aplicación cliente que envía mensajes a su centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d29dc-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="d29dc-118">Una cuenta de Power BI</span><span class="sxs-lookup"><span data-stu-id="d29dc-118">A Power BI account.</span></span> <span data-ttu-id="d29dc-119">([pruebe Power BI de manera gratuita](https://powerbi.microsoft.com/)).</span><span class="sxs-lookup"><span data-stu-id="d29dc-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="d29dc-120">Creación, configuración y ejecución de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d29dc-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="d29dc-121">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="d29dc-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="d29dc-122">En Azure Portal, haga clic en Nuevo > Internet de las cosas > Trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d29dc-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="d29dc-123">Escriba la siguiente información para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d29dc-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="d29dc-124">**Nombre del trabajo**: el nombre del trabajo.</span><span class="sxs-lookup"><span data-stu-id="d29dc-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="d29dc-125">El nombre debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="d29dc-125">The name must be globally unique.</span></span>

   <span data-ttu-id="d29dc-126">**Grupo de recursos**: use el mismo grupo de recursos que usa el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d29dc-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="d29dc-127">**Ubicación**: use la misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d29dc-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="d29dc-128">**Anclar al panel**: active esta opción para facilitar el acceso al IoT Hub desde el panel.</span><span class="sxs-lookup"><span data-stu-id="d29dc-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Creación de un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="d29dc-130">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="d29dc-131">Adición de una entrada al trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d29dc-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="d29dc-132">Abra el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d29dc-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="d29dc-133">En **Topología de trabajo**, haga clic en **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="d29dc-134">En el panel **Entradas**, haga clic en **Agregar** y, a continuación, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d29dc-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="d29dc-135">**Alias de entrada**: el alias único para la entrada.</span><span class="sxs-lookup"><span data-stu-id="d29dc-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="d29dc-136">**Origen**: seleccione **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="d29dc-137">**Grupo de consumidores**: seleccione el grupo de consumidores que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="d29dc-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="d29dc-138">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-138">Click **Create**.</span></span>

   ![Adición de una entrada a un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="d29dc-140">Adición de una salida al trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d29dc-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="d29dc-141">En **Topología de trabajo**, haga clic en **Salidas**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="d29dc-142">En el panel **Salidas**, haga clic en **Agregar** y, a continuación, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d29dc-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="d29dc-143">**Alias de salida**: el alias único para la salida.</span><span class="sxs-lookup"><span data-stu-id="d29dc-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="d29dc-144">**Receptor**: seleccione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="d29dc-145">Haga clic en **Autorizar** y, a continuación, inicie sesión en su cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="d29dc-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="d29dc-146">Una vez autorizado, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d29dc-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="d29dc-147">**Área de trabajo de grupo**: seleccione el área de trabajo de grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="d29dc-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="d29dc-148">**Nombre del conjunto de datos**: escriba un nombre para el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="d29dc-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="d29dc-149">**Nombre de la tabla**: escriba un nombre para la tabla.</span><span class="sxs-lookup"><span data-stu-id="d29dc-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="d29dc-150">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-150">Click **Create**.</span></span>

   ![Adición de una salida a un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="d29dc-152">Configuración de la consulta del trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d29dc-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="d29dc-153">En **Topología de trabajo**, haga clic en **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="d29dc-154">Reemplace `[YourInputAlias]` por el alias de entrada del trabajo.</span><span class="sxs-lookup"><span data-stu-id="d29dc-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="d29dc-155">Reemplace `[YourOutputAlias]` por el alias de salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="d29dc-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="d29dc-156">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-156">Click **Save**.</span></span>

   ![Adición de una consulta a un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="d29dc-158">Ejecución del trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="d29dc-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="d29dc-159">En el trabajo de Stream Analytics, haga clic en **Iniciar** > **Ahora** > **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="d29dc-160">Una vez que el trabajo se inicia correctamente, su estado cambia de **Detenido** a **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Ejecución de un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="d29dc-162">Creación y publicación de un informe de Power BI para visualizar los datos</span><span class="sxs-lookup"><span data-stu-id="d29dc-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="d29dc-163">Asegúrese de que la aplicación de ejemplo se ejecuta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d29dc-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="d29dc-164">Si no es así, puede hacer referencia a los tutoriales en [Configurar su dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="d29dc-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="d29dc-165">Inicie sesión en su cuenta de [Power BI](https://powerbi.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="d29dc-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="d29dc-166">Vaya al área de trabajo de grupo que estableció en el momento de crear la salida para el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d29dc-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="d29dc-167">Haga clic en **Conjuntos de datos de streaming**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="d29dc-168">Debería ver en la lista el conjunto de datos que especificó en el momento de crear la salida para el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d29dc-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="d29dc-169">En **ACCIONES**, haga clic en el primer icono para crear un informe.</span><span class="sxs-lookup"><span data-stu-id="d29dc-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Creación de informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="d29dc-171">Cree un gráfico de líneas para mostrar la temperatura en tiempo real en un período determinado.</span><span class="sxs-lookup"><span data-stu-id="d29dc-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="d29dc-172">En la página de creación de informes, agregue un gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="d29dc-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="d29dc-173">En el panel **Campos**, expanda la tabla que especificó en el momento de crear la salida para el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d29dc-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="d29dc-174">Arrastre **EventEnqueuedUtcTime** (Hora UTC de evento en cola) al **Eje** en el panel **Visualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="d29dc-175">Arrastre **temperature** (temperatura) a **Valores**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="d29dc-176">Ya se ha creado el gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="d29dc-176">Now a line chart is created.</span></span> <span data-ttu-id="d29dc-177">El eje x muestra la fecha y hora en la zona horaria UTC.</span><span class="sxs-lookup"><span data-stu-id="d29dc-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="d29dc-178">El eje y muestra la temperatura del sensor.</span><span class="sxs-lookup"><span data-stu-id="d29dc-178">The y-axis displays temperature from the sensor.</span></span>

      ![Adición de un gráfico de líneas de temperatura a un informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="d29dc-180">Cree otro gráfico de líneas para mostrar la humedad en tiempo real en un período determinado.</span><span class="sxs-lookup"><span data-stu-id="d29dc-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="d29dc-181">Para ello, siga los mismos pasos anteriores y coloque **EventEnqueuedUtcTime** (Hora UTC de evento en cola) en el eje x y **humidity** (humedad) en el eje y.</span><span class="sxs-lookup"><span data-stu-id="d29dc-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Adición de un gráfico de líneas de humedad a un informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="d29dc-183">Haga clic en **Guardar** para guardar el informe.</span><span class="sxs-lookup"><span data-stu-id="d29dc-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="d29dc-184">Haga clic en **Archivo** > **Publicar en Web**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="d29dc-185">Haga clic en **Crear código para insertar** y, a continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="d29dc-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="d29dc-186">Se le ofrecerá el vínculo del informe, que puede compartir con cualquiera para concederle acceso a este, y un fragmento de código para que pueda integrarlo en su blog o sitio web.</span><span class="sxs-lookup"><span data-stu-id="d29dc-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Publicación de informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="d29dc-188">Microsoft también ofrece las [aplicaciones móviles de Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) para ver e interactuar con los informes y paneles de Power BI desde su dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="d29dc-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d29dc-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d29dc-189">Next steps</span></span>

<span data-ttu-id="d29dc-190">Ha utilizado correctamente Power BI para visualizar datos de sensor en tiempo real desde su centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d29dc-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="d29dc-191">Hay otra manera de visualizar datos desde Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d29dc-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="d29dc-192">Consulte [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md) (Uso de Azure Web Apps para visualizar datos del sensor en tiempo real desde Azure IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="d29dc-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
