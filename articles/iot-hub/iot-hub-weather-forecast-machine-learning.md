---
title: "previsión de uso de aprendizaje automático de Azure con datos desde el centro de IoT de aaaWeather | Documentos de Microsoft"
description: "Usar aprendizaje automático de Azure toopredict Hola oportunidad de lluvia basada en humedad y temperatura Hola datos que recopila su centro de IoT de un sensor."
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
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="b8897-104">Boletín meteorológico utilizando los datos de sensor de Hola desde el centro de IoT en aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b8897-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="b8897-106">Aprendizaje automático es una técnica de ciencia de datos que ayuda a los equipos Obtenga información acerca de las tendencias, resultados y comportamientos de futuras de tooforecast de datos existente.</span><span class="sxs-lookup"><span data-stu-id="b8897-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="b8897-107">Aprendizaje automático de Azure es un servicio de análisis predictivos de nube que hace posible tooquickly crear e implementar modelos de predicción como soluciones de análisis.</span><span class="sxs-lookup"><span data-stu-id="b8897-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b8897-108">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="b8897-108">What you learn</span></span>

<span data-ttu-id="b8897-109">Obtenga información acerca cómo toouse aprendizaje automático de Azure toodo boletín meteorológico (posibilidad de lluvia) utilizando Hola temperatura y humedad datos desde el centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8897-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="b8897-110">posibilidad de Hola de lluvia es la salida de hello de un modelo de predicción meteorológica preparada.</span><span class="sxs-lookup"><span data-stu-id="b8897-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="b8897-111">modelo de Hola se basa en la posibilidad de tooforecast de datos históricos de lluvia en función de la temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="b8897-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b8897-112">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="b8897-112">What you do</span></span>

- <span data-ttu-id="b8897-113">Implementar el modelo de predicción de hello tiempo como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="b8897-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="b8897-114">Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="b8897-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="b8897-115">Crear un trabajo de análisis de transmisiones y configurar el trabajo de hello para:</span><span class="sxs-lookup"><span data-stu-id="b8897-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="b8897-116">Leer los datos de temperatura y humedad de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b8897-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="b8897-117">Llame a oportunidad de lluvia de hello web servicio tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="b8897-118">Ahorrar espacio de almacenamiento de blobs de Azure de hello resultado tooan.</span><span class="sxs-lookup"><span data-stu-id="b8897-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="b8897-119">Use Microsoft Azure Storage Explorer tooview boletín meteorológico Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b8897-120">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="b8897-120">What you need</span></span>

- <span data-ttu-id="b8897-121">Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="b8897-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="b8897-122">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b8897-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="b8897-123">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b8897-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b8897-124">Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b8897-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="b8897-125">Una cuenta de Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b8897-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="b8897-126">([Pruebe Machine Learning Studio gratis](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="b8897-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="b8897-127">Implementar el modelo de predicción de hello tiempo como un servicio web</span><span class="sxs-lookup"><span data-stu-id="b8897-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="b8897-128">Vaya toohello [página de modelo de predicción de tiempo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="b8897-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="b8897-129">Haga clic en **Abrir en Studio** en Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b8897-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="b8897-130">![Página de modelo de predicción Hola abierto el tiempo en la Galería de inteligencia de Cortana](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="b8897-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="b8897-131">Haga clic en **ejecutar** toovalidate Hola los pasos en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="b8897-132">Este paso puede tardar toocomplete de 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="b8897-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="b8897-133">![Modelo de predicción de tiempo de hello abrir en estudio de aprendizaje automático de Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="b8897-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="b8897-134">Haga clic en **CONFIGURAR SERVICIO WEB** > **Servicio web predictivo**.</span><span class="sxs-lookup"><span data-stu-id="b8897-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="b8897-135">![Implementar el modelo de predicción de tiempo de hello en estudio de aprendizaje automático de Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="b8897-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="b8897-136">En el diagrama de hello, arrastre hello **Web proporcionados por el servicio** módulo en algún lugar cerca hello **puntuar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="b8897-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="b8897-137">Conectar hello **Web proporcionados por el servicio** módulo toohello **puntuar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="b8897-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="b8897-138">![Conectar dos módulos en Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="b8897-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="b8897-139">Haga clic en **ejecutar** toovalidate Hola los pasos en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="b8897-140">Haga clic en **implementar el servicio de WEB** modelo de hello toodeploy como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="b8897-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="b8897-141">En el panel de hello del modelo de hello, descargue Hola **Excel 2010 o el libro anterior** para **solicitud/respuesta**.</span><span class="sxs-lookup"><span data-stu-id="b8897-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="b8897-142">Asegúrese de que descargue hello **Excel 2010 o el libro anterior** incluso si está ejecutando una versión posterior de Excel en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b8897-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Descargar Hola Excel para punto de conexión de respuesta de solicitud de Hola](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="b8897-144">Abra el libro de Excel de hello, tome nota de hello **dirección URL del servicio WEB** y **clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="b8897-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="b8897-145">Creación, configuración y ejecución de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b8897-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="b8897-146">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="b8897-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="b8897-147">Hola [portal de Azure](https://ms.portal.azure.com/), haga clic en **New** > **Internet de las cosas** > **trabajo de análisis de transmisiones**.</span><span class="sxs-lookup"><span data-stu-id="b8897-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="b8897-148">Escriba Hola siguiendo la información de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="b8897-149">**Nombre del trabajo**: nombre de hello del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="b8897-150">nombre de Hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="b8897-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="b8897-151">**Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b8897-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="b8897-152">**Ubicación**: Use Hola misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8897-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="b8897-153">**PIN toodashboard**: Active esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Creación de un trabajo de Stream Analytics en Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="b8897-155">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b8897-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="b8897-156">Agregar un trabajo de análisis de transmisiones de entrada toohello</span><span class="sxs-lookup"><span data-stu-id="b8897-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b8897-157">Trabajo de análisis de transmisiones de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="b8897-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b8897-158">En **Topología de trabajo**, haga clic en **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="b8897-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="b8897-159">Hola **entradas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b8897-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b8897-160">**Alias de entrada**: alias único de hello para la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="b8897-161">**Origen**: seleccione **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b8897-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="b8897-162">**Grupo de consumidores**: grupo de consumidores de hello Select que creó.</span><span class="sxs-lookup"><span data-stu-id="b8897-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de entrada toohello en Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="b8897-164">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b8897-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="b8897-165">Agregar un trabajo de análisis de transmisiones de salida toohello</span><span class="sxs-lookup"><span data-stu-id="b8897-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b8897-166">En **Topología de trabajo**, haga clic en **Salidas**.</span><span class="sxs-lookup"><span data-stu-id="b8897-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="b8897-167">Hola **salidas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b8897-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b8897-168">**Alias de salida**: alias único de hello para la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="b8897-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="b8897-169">**Receptor**: seleccione **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="b8897-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="b8897-170">**Cuenta de almacenamiento**: Hola cuenta de almacenamiento para el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b8897-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="b8897-171">Puede crear una cuenta de almacenamiento o usar una existente.</span><span class="sxs-lookup"><span data-stu-id="b8897-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="b8897-172">**Contenedor**: contenedor Hola donde se guarda el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="b8897-173">Puede crear un contenedor o usar uno existente.</span><span class="sxs-lookup"><span data-stu-id="b8897-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="b8897-174">**Formato de serialización de eventos**: seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="b8897-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de salida toohello en Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="b8897-176">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b8897-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="b8897-177">Agregar un servicio análisis de transmisiones trabajo toocall hello web implementó toohello de función</span><span class="sxs-lookup"><span data-stu-id="b8897-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="b8897-178">En **Topología de trabajo**, haga clic en **Funciones** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b8897-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="b8897-179">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b8897-179">Enter hello following information:</span></span>

   <span data-ttu-id="b8897-180">**Alias de función**: escriba `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="b8897-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="b8897-181">**Tipo de función**: seleccione **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="b8897-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="b8897-182">**Opción de importación**: seleccione **Importar de una suscripción distinta**.</span><span class="sxs-lookup"><span data-stu-id="b8897-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="b8897-183">**Dirección URL**: escriba Hola dirección URL del servicio WEB que anotó hacia abajo del libro de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="b8897-184">**Clave**: escriba Hola clave de acceso que anotó hacia abajo del libro de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de función toohello en Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="b8897-186">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b8897-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="b8897-187">Configurar consulta Hola de trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="b8897-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="b8897-188">En **Topología de trabajo**, haga clic en **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="b8897-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="b8897-189">Reemplace código existente de hello con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="b8897-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="b8897-190">Reemplace `[YourInputAlias]` con el alias de Hola de entrada de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="b8897-191">Reemplace `[YourOutputAlias]` con el alias de salida de hello de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8897-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="b8897-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b8897-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="b8897-193">Ejecutar trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="b8897-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="b8897-194">En el trabajo de análisis de transmisiones de hello, haga clic en **iniciar** > **ahora** > **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="b8897-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="b8897-195">Una vez que se inicia correctamente el trabajo de hello, cambia el estado del trabajo de Hola de **detenido** demasiado**ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="b8897-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Ejecutar trabajo de análisis de transmisiones de Hola](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="b8897-197">Use Microsoft Azure Storage Explorer tooview boletín meteorológico Hola</span><span class="sxs-lookup"><span data-stu-id="b8897-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="b8897-198">Ejecute toostart de aplicación de cliente de hello recopilar y enviar la temperatura y humedad centro de IoT de tooyour de datos.</span><span class="sxs-lookup"><span data-stu-id="b8897-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="b8897-199">Para cada mensaje que recibe de su centro de IoT, trabajo de análisis de transmisiones de hello llama Hola boletín meteorológico web servicio tooproduce Hola posibilidad de lluvia.</span><span class="sxs-lookup"><span data-stu-id="b8897-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="b8897-200">a continuación, se guarda el resultado de Hello tooyour almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8897-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="b8897-201">Explorador de almacenamiento de Azure es una herramienta que puede usar el resultado de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="b8897-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="b8897-202">[Descargue e instale el Explorador de Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b8897-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="b8897-203">Abra el Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b8897-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="b8897-204">Inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8897-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="b8897-205">Seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b8897-205">Select your subscription.</span></span>
1. <span data-ttu-id="b8897-206">Haga clic en la suscripción > **Cuentas de almacenamiento** > su cuenta de almacenamiento > **Contenedores de blob** > su contenedor.</span><span class="sxs-lookup"><span data-stu-id="b8897-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="b8897-207">Abrir un resultado de hello de toosee de archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="b8897-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="b8897-208">registros de columna último Hola Hola posibilidad de lluvia.</span><span class="sxs-lookup"><span data-stu-id="b8897-208">hello last column records hello chance of rain.</span></span>

   ![Obtención del resultado del pronóstico meteorológico con Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="b8897-210">Resumen</span><span class="sxs-lookup"><span data-stu-id="b8897-210">Summary</span></span>

<span data-ttu-id="b8897-211">Posibilidad de hello tooproduce de aprendizaje automático de Azure de lluvia basado en datos de temperatura y humedad de Hola que recibe de su centro de IoT se usó correctamente.</span><span class="sxs-lookup"><span data-stu-id="b8897-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]