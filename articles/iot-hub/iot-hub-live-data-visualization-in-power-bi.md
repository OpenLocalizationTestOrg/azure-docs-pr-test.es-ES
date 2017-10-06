---
title: "Visualización de los datos de sensor de centro de IoT de Azure: Power BI tiempo aaaReal | Documentos de Microsoft"
description: "Usar Power BI toovisualize temperatura y humedad datos que se recopilan del sensor de Hola y envía el centro de IoT de Azure de tooyour."
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
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="caaae-104">Visualización de datos del sensor en tiempo real desde Azure IoT Hub mediante Power BI</span><span class="sxs-lookup"><span data-stu-id="caaae-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="caaae-106">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="caaae-106">What you learn</span></span>

<span data-ttu-id="caaae-107">Aprenderá cómo toovisualize en tiempo real datos del sensor que recibe de su centro de IoT de Azure por Power BI.</span><span class="sxs-lookup"><span data-stu-id="caaae-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="caaae-108">Si desea tootry visualizar datos de hello en el centro de IoT con las aplicaciones Web, consulte [datos de sensor en tiempo real de toovisualize de aplicaciones Web de Azure de uso del centro de IoT de Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="caaae-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="caaae-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="caaae-109">What you do</span></span>

- <span data-ttu-id="caaae-110">Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="caaae-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="caaae-111">Crear, configurar y ejecutar un trabajo de análisis de transmisiones de transferencia de datos desde su tooyour de centro de IoT cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="caaae-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="caaae-112">Crear y publicar los datos de hello Power BI informe toovisualize.</span><span class="sxs-lookup"><span data-stu-id="caaae-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="caaae-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="caaae-113">What you need</span></span>

- <span data-ttu-id="caaae-114">Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="caaae-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="caaae-115">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="caaae-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="caaae-116">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="caaae-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="caaae-117">Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="caaae-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="caaae-118">Una cuenta de Power BI</span><span class="sxs-lookup"><span data-stu-id="caaae-118">A Power BI account.</span></span> <span data-ttu-id="caaae-119">([pruebe Power BI de manera gratuita](https://powerbi.microsoft.com/)).</span><span class="sxs-lookup"><span data-stu-id="caaae-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="caaae-120">Creación, configuración y ejecución de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="caaae-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="caaae-121">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="caaae-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="caaae-122">En el portal de Azure de Hola, haga clic en Nuevo > Internet de las cosas > análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="caaae-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="caaae-123">Escriba Hola siguiendo la información de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="caaae-124">**Nombre del trabajo**: nombre de hello del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="caaae-125">nombre de Hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="caaae-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="caaae-126">**Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="caaae-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="caaae-127">**Ubicación**: Use Hola misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="caaae-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="caaae-128">**PIN toodashboard**: Active esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Creación de un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="caaae-130">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="caaae-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="caaae-131">Agregar un trabajo de análisis de transmisiones de entrada toohello</span><span class="sxs-lookup"><span data-stu-id="caaae-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="caaae-132">Trabajo de análisis de transmisiones de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="caaae-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="caaae-133">En **Topología de trabajo**, haga clic en **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="caaae-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="caaae-134">Hola **entradas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="caaae-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="caaae-135">**Alias de entrada**: alias único de hello para la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="caaae-136">**Origen**: seleccione **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="caaae-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="caaae-137">**Grupo de consumidores**: grupo de consumidores de hello Select que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="caaae-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="caaae-138">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="caaae-138">Click **Create**.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de entrada tooa en Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="caaae-140">Agregar un trabajo de análisis de transmisiones de salida toohello</span><span class="sxs-lookup"><span data-stu-id="caaae-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="caaae-141">En **Topología de trabajo**, haga clic en **Salidas**.</span><span class="sxs-lookup"><span data-stu-id="caaae-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="caaae-142">Hola **salidas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="caaae-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="caaae-143">**Alias de salida**: alias único de hello para la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="caaae-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="caaae-144">**Receptor**: seleccione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="caaae-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="caaae-145">Haga clic en **Autorizar** y, a continuación, inicie sesión en su cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="caaae-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="caaae-146">Una vez autorizados, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="caaae-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="caaae-147">**Área de trabajo de grupo**: seleccione el área de trabajo de grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="caaae-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="caaae-148">**Nombre del conjunto de datos**: escriba un nombre para el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="caaae-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="caaae-149">**Nombre de la tabla**: escriba un nombre para la tabla.</span><span class="sxs-lookup"><span data-stu-id="caaae-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="caaae-150">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="caaae-150">Click **Create**.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de salida tooa en Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="caaae-152">Configurar consulta Hola de trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="caaae-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="caaae-153">En **Topología de trabajo**, haga clic en **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="caaae-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="caaae-154">Reemplace `[YourInputAlias]` con el alias de Hola de entrada de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="caaae-155">Reemplace `[YourOutputAlias]` con el alias de salida de hello de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="caaae-156">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="caaae-156">Click **Save**.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de consulta tooa en Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="caaae-158">Ejecutar trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="caaae-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="caaae-159">En el trabajo de análisis de transmisiones de hello, haga clic en **iniciar** > **ahora** > **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="caaae-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="caaae-160">Una vez que se inicia correctamente el trabajo de hello, cambia el estado del trabajo de Hola de **detenido** demasiado**ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="caaae-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Ejecución de un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="caaae-162">Crear y publicar los datos de hello Power BI informe toovisualize</span><span class="sxs-lookup"><span data-stu-id="caaae-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="caaae-163">Asegúrese de que está ejecutando la aplicación de ejemplo de Hola en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="caaae-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="caaae-164">Si no es así, puede hacer referencia a los tutoriales de toohello en [configurar su dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="caaae-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="caaae-165">Inicie sesión en tooyour [Power BI](https://powerbi.microsoft.com/en-us/) cuenta.</span><span class="sxs-lookup"><span data-stu-id="caaae-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="caaae-166">Vaya el área de trabajo de grupo de toohello que estableciste cuando creaste la salida de hello para el trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="caaae-167">Haga clic en **Conjuntos de datos de streaming**.</span><span class="sxs-lookup"><span data-stu-id="caaae-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="caaae-168">Debería ver conjunto de datos de hello muestran que especificó cuando creó Hola de salida de trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="caaae-169">En **acciones**, haga clic en el primer icono toocreate un informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Creación de informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="caaae-171">Cree una temperatura de línea gráfico tooshow en tiempo real con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="caaae-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="caaae-172">En la página de creación de informes de hello, agregue un gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="caaae-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="caaae-173">En hello **campos** panel, expanda la tabla de Hola que especificó cuando creó la salida de hello para el trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="caaae-174">Arrastre **EventEnqueuedUtcTime** demasiado**eje** en hello **visualizaciones** panel.</span><span class="sxs-lookup"><span data-stu-id="caaae-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="caaae-175">Arrastre **temperatura** demasiado**valores**.</span><span class="sxs-lookup"><span data-stu-id="caaae-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="caaae-176">Ya se ha creado el gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="caaae-176">Now a line chart is created.</span></span> <span data-ttu-id="caaae-177">eje x de Hello muestra la fecha y hora en la zona horaria de hello UTC.</span><span class="sxs-lookup"><span data-stu-id="caaae-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="caaae-178">eje y Hello muestra la temperatura del sensor de Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Agregar un gráfico de líneas para temperatura tooa informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="caaae-180">Cree otro humedad en tiempo real de línea gráfico tooshow con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="caaae-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="caaae-181">toodo esto, siga Hola mismo pasos anteriormente y coloque **EventEnqueuedUtcTime** en el eje x de Hola y **humedad** en el eje y Hola.</span><span class="sxs-lookup"><span data-stu-id="caaae-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Agregar un gráfico de líneas para humedad tooa informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="caaae-183">Haga clic en **guardar** informe de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="caaae-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="caaae-184">Haga clic en **archivo** > **publicar tooweb**.</span><span class="sxs-lookup"><span data-stu-id="caaae-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="caaae-185">Haga clic en **Crear código para insertar** y, a continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="caaae-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="caaae-186">Se le ofrece el vínculo de informe de Hola que puede compartir con cualquiera de acceso a los informes y un informe de Hola de toointegrate de fragmento de código en su blog o sitio Web.</span><span class="sxs-lookup"><span data-stu-id="caaae-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Publicación de informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="caaae-188">Microsoft también ofrece hello [aplicaciones móviles de Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) para ver e interactuar con los informes y paneles de Power BI en su dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="caaae-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caaae-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="caaae-189">Next steps</span></span>

<span data-ttu-id="caaae-190">Ha usado correctamente datos de Power BI toovisualize sensor en tiempo real desde su centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="caaae-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="caaae-191">Hay un dato de toovisualize forma alternativa de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="caaae-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="caaae-192">Vea [datos de sensor en tiempo real de toovisualize de aplicaciones Web de Azure de uso del centro de IoT de Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="caaae-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
