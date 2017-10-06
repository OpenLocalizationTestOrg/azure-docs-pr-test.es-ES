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
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>Visualización de datos del sensor en tiempo real desde Azure IoT Hub mediante Power BI

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>Conocimientos que adquirirá

Aprenderá cómo toovisualize en tiempo real datos del sensor que recibe de su centro de IoT de Azure por Power BI. Si desea tootry visualizar datos de hello en el centro de IoT con las aplicaciones Web, consulte [datos de sensor en tiempo real de toovisualize de aplicaciones Web de Azure de uso del centro de IoT de Azure](iot-hub-live-data-visualization-in-web-apps.md).

## <a name="what-you-do"></a>Qué debe hacer

- Preparar el IoT Hub para el acceso a datos mediante la adición de un grupo de consumidores.
- Crear, configurar y ejecutar un trabajo de análisis de transmisiones de transferencia de datos desde su tooyour de centro de IoT cuenta de Power BI.
- Crear y publicar los datos de hello Power BI informe toovisualize.

## <a name="what-you-need"></a>Lo que necesita

- Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:
  - Una suscripción de Azure activa.
  - Un centro de Azure IoT en su suscripción.
  - Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.
- Una cuenta de Power BI ([pruebe Power BI de manera gratuita](https://powerbi.microsoft.com/)).

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Creación, configuración y ejecución de un trabajo de Stream Analytics

### <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones

1. En el portal de Azure de Hola, haga clic en Nuevo > Internet de las cosas > análisis de transmisiones.
1. Escriba Hola siguiendo la información de trabajo de Hola.

   **Nombre del trabajo**: nombre de hello del trabajo de Hola. nombre de Hello debe ser único globalmente.

   **Grupo de recursos**: Use Hola mismo grupo de recursos que usa el centro de IoT.

   **Ubicación**: Use Hola misma ubicación que el grupo de recursos.

   **PIN toodashboard**: Active esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.

   ![Creación de un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. Haga clic en **Crear**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Agregar un trabajo de análisis de transmisiones de entrada toohello

1. Trabajo de análisis de transmisiones de hello abierto.
1. En **Topología de trabajo**, haga clic en **Entradas**.
1. Hola **entradas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:

   **Alias de entrada**: alias único de hello para la entrada de Hola.

   **Origen**: seleccione **IoT Hub**.

   **Grupo de consumidores**: grupo de consumidores de hello Select que acaba de crear.
1. Haga clic en **Crear**.

   ![Agregar un trabajo de análisis de transmisiones de entrada tooa en Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>Agregar un trabajo de análisis de transmisiones de salida toohello

1. En **Topología de trabajo**, haga clic en **Salidas**.
1. Hola **salidas** panel, haga clic en **agregar**y, a continuación, escriba Hola siguiente información:

   **Alias de salida**: alias único de hello para la salida de hello.

   **Receptor**: seleccione **Power BI**.
1. Haga clic en **Autorizar** y, a continuación, inicie sesión en su cuenta de Power BI.
1. Una vez autorizados, escriba Hola siguiente información:

   **Área de trabajo de grupo**: seleccione el área de trabajo de grupo de destino.

   **Nombre del conjunto de datos**: escriba un nombre para el conjunto de datos.

   **Nombre de la tabla**: escriba un nombre para la tabla.
1. Haga clic en **Crear**.

   ![Agregar un trabajo de análisis de transmisiones de salida tooa en Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Configurar consulta Hola de trabajo de análisis de transmisiones de Hola

1. En **Topología de trabajo**, haga clic en **Consulta**.
1. Reemplace `[YourInputAlias]` con el alias de Hola de entrada de trabajo de Hola.
1. Reemplace `[YourOutputAlias]` con el alias de salida de hello de trabajo de Hola.
1. Haga clic en **Guardar**.

   ![Agregar un trabajo de análisis de transmisiones de consulta tooa en Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>Ejecutar trabajo de análisis de transmisiones de Hola

En el trabajo de análisis de transmisiones de hello, haga clic en **iniciar** > **ahora** > **iniciar**. Una vez que se inicia correctamente el trabajo de hello, cambia el estado del trabajo de Hola de **detenido** demasiado**ejecutando**.

![Ejecución de un trabajo de Stream Analytics en Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>Crear y publicar los datos de hello Power BI informe toovisualize

1. Asegúrese de que está ejecutando la aplicación de ejemplo de Hola en el dispositivo. Si no es así, puede hacer referencia a los tutoriales de toohello en [configurar su dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).
1. Inicie sesión en tooyour [Power BI](https://powerbi.microsoft.com/en-us/) cuenta.
1. Vaya el área de trabajo de grupo de toohello que estableciste cuando creaste la salida de hello para el trabajo de análisis de transmisiones de Hola.
1. Haga clic en **Conjuntos de datos de streaming**.

   Debería ver conjunto de datos de hello muestran que especificó cuando creó Hola de salida de trabajo de análisis de transmisiones de Hola.
1. En **acciones**, haga clic en el primer icono toocreate un informe de Hola.

   ![Creación de informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. Cree una temperatura de línea gráfico tooshow en tiempo real con el tiempo.
   1. En la página de creación de informes de hello, agregue un gráfico de líneas.
   1. En hello **campos** panel, expanda la tabla de Hola que especificó cuando creó la salida de hello para el trabajo de análisis de transmisiones de Hola.
   1. Arrastre **EventEnqueuedUtcTime** demasiado**eje** en hello **visualizaciones** panel.
   1. Arrastre **temperatura** demasiado**valores**.

      Ya se ha creado el gráfico de líneas. eje x de Hello muestra la fecha y hora en la zona horaria de hello UTC. eje y Hello muestra la temperatura del sensor de Hola.

      ![Agregar un gráfico de líneas para temperatura tooa informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. Cree otro humedad en tiempo real de línea gráfico tooshow con el tiempo. toodo esto, siga Hola mismo pasos anteriormente y coloque **EventEnqueuedUtcTime** en el eje x de Hola y **humedad** en el eje y Hola.

   ![Agregar un gráfico de líneas para humedad tooa informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. Haga clic en **guardar** informe de hello toosave.
1. Haga clic en **archivo** > **publicar tooweb**.
1. Haga clic en **Crear código para insertar** y, a continuación, haga clic en **Publicar**.

Se le ofrece el vínculo de informe de Hola que puede compartir con cualquiera de acceso a los informes y un informe de Hola de toointegrate de fragmento de código en su blog o sitio Web.

![Publicación de informe de Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft también ofrece hello [aplicaciones móviles de Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) para ver e interactuar con los informes y paneles de Power BI en su dispositivo móvil.

## <a name="next-steps"></a>Pasos siguientes

Ha usado correctamente datos de Power BI toovisualize sensor en tiempo real desde su centro de IoT de Azure.
Hay un dato de toovisualize forma alternativa de centro de IoT de Azure. Vea [datos de sensor en tiempo real de toovisualize de aplicaciones Web de Azure de uso del centro de IoT de Azure](iot-hub-live-data-visualization-in-web-apps.md).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
