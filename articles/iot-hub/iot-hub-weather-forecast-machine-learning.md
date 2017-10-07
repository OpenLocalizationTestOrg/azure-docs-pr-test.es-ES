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
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Boletín meteorológico utilizando los datos de sensor de Hola desde el centro de IoT en aprendizaje automático de Azure

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Aprendizaje automático es una técnica de ciencia de datos que ayuda a los equipos Obtenga información acerca de las tendencias, resultados y comportamientos de futuras de tooforecast de datos existente. Aprendizaje automático de Azure es un servicio de análisis predictivos de nube que hace posible tooquickly crear e implementar modelos de predicción como soluciones de análisis.

## <a name="what-you-learn"></a>Conocimientos que adquirirá

Obtenga información acerca cómo toouse aprendizaje automático de Azure toodo boletín meteorológico (posibilidad de lluvia) utilizando Hola temperatura y humedad datos desde el centro de IoT de Azure. posibilidad de Hola de lluvia es la salida de hello de un modelo de predicción meteorológica preparada. modelo de Hola se basa en la posibilidad de tooforecast de datos históricos de lluvia en función de la temperatura y humedad.

## <a name="what-you-do"></a>Qué debe hacer

- Implementar el modelo de predicción de hello tiempo como un servicio web.
- Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.
- Crear un trabajo de análisis de transmisiones y configurar el trabajo de hello para:
  - Leer los datos de temperatura y humedad de IoT Hub.
  - Llame a oportunidad de lluvia de hello web servicio tooget Hola.
  - Ahorrar espacio de almacenamiento de blobs de Azure de hello resultado tooan.
- Use Microsoft Azure Storage Explorer tooview boletín meteorológico Hola.

## <a name="what-you-need"></a>Lo que necesita

- Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:
  - Una suscripción de Azure activa.
  - Un centro de Azure IoT en su suscripción.
  - Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.
- Una cuenta de Azure Machine Learning Studio. ([Pruebe Machine Learning Studio gratis](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Implementar el modelo de predicción de hello tiempo como un servicio web

1. Vaya toohello [página de modelo de predicción de tiempo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Haga clic en **Abrir en Studio** en Microsoft Azure Machine Learning Studio.
   ![Página de modelo de predicción Hola abierto el tiempo en la Galería de inteligencia de Cortana](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Haga clic en **ejecutar** toovalidate Hola los pasos en el modelo de Hola. Este paso puede tardar toocomplete de 2 minutos.
   ![Modelo de predicción de tiempo de hello abrir en estudio de aprendizaje automático de Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Haga clic en **CONFIGURAR SERVICIO WEB** > **Servicio web predictivo**.
   ![Implementar el modelo de predicción de tiempo de hello en estudio de aprendizaje automático de Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. En el diagrama de hello, arrastre hello **Web proporcionados por el servicio** módulo en algún lugar cerca hello **puntuar modelo** módulo.
1. Conectar hello **Web proporcionados por el servicio** módulo toohello **puntuar modelo** módulo.
   ![Conectar dos módulos en Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Haga clic en **ejecutar** toovalidate Hola los pasos en el modelo de Hola.
1. Haga clic en **implementar el servicio de WEB** modelo de hello toodeploy como un servicio web.
1. En el panel de hello del modelo de hello, descargue Hola **Excel 2010 o el libro anterior** para **solicitud/respuesta**.

   > [!Note]
   > Asegúrese de que descargue hello **Excel 2010 o el libro anterior** incluso si está ejecutando una versión posterior de Excel en el equipo.

   ![Descargar Hola Excel para punto de conexión de respuesta de solicitud de Hola](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Abra el libro de Excel de hello, tome nota de hello **dirección URL del servicio WEB** y **clave de acceso**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Creación, configuración y ejecución de un trabajo de Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones

1. Hola [portal de Azure](https://ms.portal.azure.com/), haga clic en **New** > **Internet de las cosas** > **trabajo de análisis de transmisiones**.
1. Escriba Hola siguiendo la información de trabajo de Hola.

   **Nombre del trabajo**: nombre de hello del trabajo de Hola. nombre de Hello debe ser único globalmente.

   **Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.

   **Ubicación**: Use Hola misma ubicación que el grupo de recursos.

   **PIN toodashboard**: Active esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.

   ![Creación de un trabajo de Stream Analytics en Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Haga clic en **Crear**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Agregar un trabajo de análisis de transmisiones de entrada toohello

1. Trabajo de análisis de transmisiones de hello abierto.
1. En **Topología de trabajo**, haga clic en **Entradas**.
1. Hola **entradas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:

   **Alias de entrada**: alias único de hello para la entrada de Hola.

   **Origen**: seleccione **IoT Hub**.

   **Grupo de consumidores**: grupo de consumidores de hello Select que creó.

   ![Agregar un trabajo de análisis de transmisiones de entrada toohello en Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Haga clic en **Crear**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Agregar un trabajo de análisis de transmisiones de salida toohello

1. En **Topología de trabajo**, haga clic en **Salidas**.
1. Hola **salidas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:

   **Alias de salida**: alias único de hello para la salida de hello.

   **Receptor**: seleccione **Blob Storage**.

   **Cuenta de almacenamiento**: Hola cuenta de almacenamiento para el almacenamiento de blobs. Puede crear una cuenta de almacenamiento o usar una existente.

   **Contenedor**: contenedor Hola donde se guarda el blob de Hola. Puede crear un contenedor o usar uno existente.

   **Formato de serialización de eventos**: seleccione **CSV**.

   ![Agregar un trabajo de análisis de transmisiones de salida toohello en Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Haga clic en **Crear**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Agregar un servicio análisis de transmisiones trabajo toocall hello web implementó toohello de función

1. En **Topología de trabajo**, haga clic en **Funciones** > **Agregar**.
1. Escriba Hola siguiente información:

   **Alias de función**: escriba `machinelearning`.

   **Tipo de función**: seleccione **Azure ML**.

   **Opción de importación**: seleccione **Importar de una suscripción distinta**.

   **Dirección URL**: escriba Hola dirección URL del servicio WEB que anotó hacia abajo del libro de Excel de Hola.

   **Clave**: escriba Hola clave de acceso que anotó hacia abajo del libro de Excel de Hola.

   ![Agregar un trabajo de análisis de transmisiones de función toohello en Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Haga clic en **Crear**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurar consulta Hola de trabajo de análisis de transmisiones de Hola

1. En **Topología de trabajo**, haga clic en **Consulta**.
1. Reemplace código existente de hello con hello siguiente código:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Reemplace `[YourInputAlias]` con el alias de Hola de entrada de trabajo de Hola.

   Reemplace `[YourOutputAlias]` con el alias de salida de hello de trabajo de Hola.

1. Haga clic en **Guardar**.

### <a name="run-hello-stream-analytics-job"></a>Ejecutar trabajo de análisis de transmisiones de Hola

En el trabajo de análisis de transmisiones de hello, haga clic en **iniciar** > **ahora** > **iniciar**. Una vez que se inicia correctamente el trabajo de hello, cambia el estado del trabajo de Hola de **detenido** demasiado**ejecutando**.

![Ejecutar trabajo de análisis de transmisiones de Hola](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Use Microsoft Azure Storage Explorer tooview boletín meteorológico Hola

Ejecute toostart de aplicación de cliente de hello recopilar y enviar la temperatura y humedad centro de IoT de tooyour de datos. Para cada mensaje que recibe de su centro de IoT, trabajo de análisis de transmisiones de hello llama Hola boletín meteorológico web servicio tooproduce Hola posibilidad de lluvia. a continuación, se guarda el resultado de Hello tooyour almacenamiento de blobs de Azure. Explorador de almacenamiento de Azure es una herramienta que puede usar el resultado de hello tooview.

1. [Descargue e instale el Explorador de Microsoft Azure Storage](http://storageexplorer.com/).
1. Abra el Explorador de Azure Storage.
1. Inicie sesión en tooyour cuenta de Azure.
1. Seleccione su suscripción.
1. Haga clic en la suscripción > **Cuentas de almacenamiento** > su cuenta de almacenamiento > **Contenedores de blob** > su contenedor.
1. Abrir un resultado de hello de toosee de archivo CSV. registros de columna último Hola Hola posibilidad de lluvia.

   ![Obtención del resultado del pronóstico meteorológico con Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Resumen

Posibilidad de hello tooproduce de aprendizaje automático de Azure de lluvia basado en datos de temperatura y humedad de Hola que recibe de su centro de IoT se usó correctamente.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]