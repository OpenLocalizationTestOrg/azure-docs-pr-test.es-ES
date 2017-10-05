---
title: "Pronóstico meteorológico mediante la utilización de Azure Machine Learning con datos de IoT Hub | Microsoft Docs"
description: "Use Azure Machine Learning para predecir la posibilidad de lluvia en función de los datos de temperatura y humedad que IoT Hub recopila de un sensor."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Previsión meteorológica con Machine Learning"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="2e6a3-104">Pronóstico meteorológico con los datos del sensor de IoT Hub en Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2e6a3-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="2e6a3-106">El aprendizaje automático es una técnica de ciencia de datos que ayuda a los equipos a aprender de los datos existentes para prever tendencias, resultados y comportamientos futuros.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="2e6a3-107">Azure Machine Learning es un servicio de análisis predictivo en la nube que permite crear e implementar rápidamente modelos predictivos como soluciones de análisis.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2e6a3-108">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="2e6a3-108">What you learn</span></span>

<span data-ttu-id="2e6a3-109">Obtenga información sobre cómo usar Azure Machine Learning para realizar pronósticos meteorológicos, como la posibilidad de lluvia, con los datos de temperatura y humedad de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="2e6a3-110">La posibilidad de lluvia es el resultado de un modelo de pronóstico meteorológico preparado.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="2e6a3-111">El modelo se basa en datos históricos para predecir la posibilidad de lluvia en función de la temperatura y la humedad.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2e6a3-112">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="2e6a3-112">What you do</span></span>

- <span data-ttu-id="2e6a3-113">Implementar el modelo de pronóstico meteorológico como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="2e6a3-114">Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="2e6a3-115">Crear un trabajo de Stream Analytics y configurar el trabajo para:</span><span class="sxs-lookup"><span data-stu-id="2e6a3-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="2e6a3-116">Leer los datos de temperatura y humedad de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="2e6a3-117">Llamar al servicio web para saber la posibilidad de lluvia.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="2e6a3-118">Guardar el resultado en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="2e6a3-119">Usar el Explorador de Microsoft Azure Storage para consultar el pronóstico meteorológico.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2e6a3-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="2e6a3-120">What you need</span></span>

- <span data-ttu-id="2e6a3-121">Tutorial [Instalación de su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde se abordan los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="2e6a3-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="2e6a3-122">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="2e6a3-123">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="2e6a3-124">Una aplicación cliente que envía mensajes a su centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="2e6a3-125">Una cuenta de Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="2e6a3-126">([Pruebe Machine Learning Studio gratis](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="2e6a3-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="2e6a3-127">Implementación del modelo de pronóstico meteorológico como un servicio web</span><span class="sxs-lookup"><span data-stu-id="2e6a3-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="2e6a3-128">Vaya a la [página del modelo de pronóstico meteorológico](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="2e6a3-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="2e6a3-129">Haga clic en **Abrir en Studio** en Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="2e6a3-130">![Abrir la página del modelo de pronóstico meteorológico en la Galería de Cortana Intelligence](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="2e6a3-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="2e6a3-131">Haga clic en **Ejecutar** para validar los pasos del modelo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="2e6a3-132">Este paso puede tardar 2 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="2e6a3-133">![Abrir el modelo de pronóstico meteorológico en Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="2e6a3-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="2e6a3-134">Haga clic en **CONFIGURAR SERVICIO WEB** > **Servicio web predictivo**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="2e6a3-135">![Implementar el modelo de pronóstico meteorológico en Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="2e6a3-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="2e6a3-136">En el diagrama, arrastre el módulo **Entrada de servicio web** a algún lugar cerca del módulo **Puntuar modelo**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="2e6a3-137">Conecte el módulo **Entrada de servicio web** con el módulo **Puntuar modelo**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="2e6a3-138">![Conectar dos módulos en Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="2e6a3-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="2e6a3-139">Haga clic en **EJECUTAR** para validar los pasos del modelo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="2e6a3-140">Haga clic en **IMPLEMENTAR SERVICIO WEB** para implementar el modelo como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="2e6a3-141">En el panel del modelo, descargue **Excel 2010 o el libro anterior** para **SOLICITUD/RESPUESTA**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="2e6a3-142">Asegúrese de descargar **Excel 2010 o el libro anterior** aunque ejecute la última versión de Excel en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Descargar Excel para el punto de conexión SOLICITUD/RESPUESTA](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="2e6a3-144">Abra el libro de Excel, tome nota de la **DIRECCIÓN URL DEL SERVICIO WEB** y de la **CLAVE DE ACCESO**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="2e6a3-145">Creación, configuración y ejecución de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e6a3-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="2e6a3-146">Creación de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e6a3-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="2e6a3-147">En [Azure Portal](https://ms.portal.azure.com/), haga clic en **Nuev** > **Internet de las cosas** > **Trabajo de Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="2e6a3-148">Escriba la siguiente información para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="2e6a3-149">**Nombre del trabajo**: el nombre del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="2e6a3-150">El nombre debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-150">The name must be globally unique.</span></span>

   <span data-ttu-id="2e6a3-151">**Grupo de recursos**: use el mismo grupo de recursos que usa el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="2e6a3-152">**Ubicación**: use la misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="2e6a3-153">**Anclar al panel**: active esta opción para facilitar el acceso al IoT Hub desde el panel.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Creación de un trabajo de Stream Analytics en Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="2e6a3-155">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="2e6a3-156">Adición de una entrada al trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e6a3-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="2e6a3-157">Abra el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="2e6a3-158">En **Topología de trabajo**, haga clic en **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="2e6a3-159">En el panel **Entradas**, haga clic en **Agregar** y, a continuación, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="2e6a3-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="2e6a3-160">**Alias de entrada**: el alias único para la entrada.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="2e6a3-161">**Origen**: seleccione **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="2e6a3-162">**Grupo de consumidores**: seleccione el grupo de consumidores que ha creado.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Adición de una entrada al trabajo de Stream Analytics en Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="2e6a3-164">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="2e6a3-165">Adición de una salida al trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e6a3-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="2e6a3-166">En **Topología de trabajo**, haga clic en **Salidas**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="2e6a3-167">En el panel **Salidas**, haga clic en **Agregar** y, a continuación, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="2e6a3-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="2e6a3-168">**Alias de salida**: el alias único para la salida.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="2e6a3-169">**Receptor**: seleccione **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="2e6a3-170">**Cuenta de almacenamiento**: la cuenta de almacenamiento para Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="2e6a3-171">Puede crear una cuenta de almacenamiento o usar una existente.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="2e6a3-172">**Contenedor**: el contenedor donde se guarda el blob.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="2e6a3-173">Puede crear un contenedor o usar uno existente.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="2e6a3-174">**Formato de serialización de eventos**: seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Adición de una salida al trabajo de Stream Analytics en Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="2e6a3-176">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="2e6a3-177">Adición de una función al trabajo de Stream Analytics para llamar al servicio web implementado</span><span class="sxs-lookup"><span data-stu-id="2e6a3-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="2e6a3-178">En **Topología de trabajo**, haga clic en **Funciones** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="2e6a3-179">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="2e6a3-179">Enter the following information:</span></span>

   <span data-ttu-id="2e6a3-180">**Alias de función**: escriba `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="2e6a3-181">**Tipo de función**: seleccione **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="2e6a3-182">**Opción de importación**: seleccione **Importar de una suscripción distinta**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="2e6a3-183">**Dirección URL**: escriba la DIRECCIÓN URL DEL SERVICIO WEB que anotó del libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="2e6a3-184">**Clave**: escriba la CLAVE DE ACCESO que anotó del libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Adición de una función al trabajo de Stream Analytics en Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="2e6a3-186">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="2e6a3-187">Configuración de la consulta del trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e6a3-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="2e6a3-188">En **Topología de trabajo**, haga clic en **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="2e6a3-189">Reemplace el código existente por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="2e6a3-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="2e6a3-190">Reemplace `[YourInputAlias]` por el alias de entrada del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="2e6a3-191">Reemplace `[YourOutputAlias]` por el alias de salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="2e6a3-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="2e6a3-193">Ejecución del trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e6a3-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="2e6a3-194">En el trabajo de Stream Analytics, haga clic en **Iniciar** > **Ahora** > **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="2e6a3-195">Una vez que el trabajo se inicia correctamente, su estado cambia de **Detenido** a **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Ejecución del trabajo de Stream Analytics](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="2e6a3-197">Uso del Explorador de Microsoft Azure Storage para consultar el pronóstico meteorológico</span><span class="sxs-lookup"><span data-stu-id="2e6a3-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="2e6a3-198">Ejecute la aplicación cliente para empezar a recopilar y enviar datos de temperatura y humedad a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="2e6a3-199">Por cada mensaje que IoT Hub recibe, el trabajo de Stream Analytics llama al servicio web de pronóstico meteorológico para producir la posibilidad de lluvia.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="2e6a3-200">El resultado se guarda luego en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="2e6a3-201">El Explorador de Azure Storage es una herramienta que puede usar para consultar el resultado.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="2e6a3-202">[Descargue e instale el Explorador de Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="2e6a3-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="2e6a3-203">Abra el Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="2e6a3-204">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="2e6a3-205">Seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-205">Select your subscription.</span></span>
1. <span data-ttu-id="2e6a3-206">Haga clic en la suscripción > **Cuentas de almacenamiento** > su cuenta de almacenamiento > **Contenedores de blob** > su contenedor.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="2e6a3-207">Abra un archivo .csv para ver el resultado.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="2e6a3-208">La última columna registra la posibilidad de lluvia.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-208">The last column records the chance of rain.</span></span>

   ![Obtención del resultado del pronóstico meteorológico con Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="2e6a3-210">Resumen</span><span class="sxs-lookup"><span data-stu-id="2e6a3-210">Summary</span></span>

<span data-ttu-id="2e6a3-211">Ha usado Azure Machine Learning correctamente para predecir la posibilidad de lluvia en función de los datos de temperatura y humedad que IoT Hub recibe.</span><span class="sxs-lookup"><span data-stu-id="2e6a3-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]