---
title: "aaaAzure modelo de datos de telemetría de aplicación visión - métrica de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de métricas"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Telemetría de métricas: modelo de datos de Application Insights

Hay dos tipos de telemetría de métricas compatibles con [Application Insights](app-insights-overview.md): la medida única y la métrica previamente agregada. La medida única es simplemente un nombre y un valor. Métrica previamente agregado especifica un valor mínimo y máximo de métrica de hello en el intervalo de agregación de Hola y desviación estándar del mismo.

La telemetría de métricas previamente agregadas da por supuesto que el período de agregación es de un minuto.

Hay varios nombres de métrica conocidos compatibles con Application Insights. 

Métricas que representan los contadores del sistema y de procesos:

| **Nombre de .NET**             | **Nombre independiente de la plataforma** | **Nombre de API DE REST** | **Descripción**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Trabajo en curso... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | CPU total del equipo
| `\Memory\Available Bytes`                 | Trabajo en curso... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | memoria disponible en disco
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Trabajo en curso... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | CPU del proceso de hello hospeda aplicación hello
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Trabajo en curso... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | memoria utilizada por el proceso de Hola que se hospeda la aplicación hello
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Trabajo en curso... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | tasa de operaciones de E/S se ejecuta por proceso que hospeda la aplicación hello
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Trabajo en curso... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | tasa de solicitudes procesadas por la aplicación 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Trabajo en curso... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | velocidad de las excepciones producidas por la aplicación
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Trabajo en curso... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | tiempo medio de ejecución de solicitudes
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Trabajo en curso... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | número de peticiones en espera de hello en una cola de procesamiento

## <a name="name"></a>Nombre

Nombre de métrica de hello le gustaría toosee en el portal de Application Insights y la interfaz de usuario. 

## <a name="value"></a>Valor

Valor único para la medida. Suma de las mediciones individuales para la agregación de Hola.

## <a name="count"></a>Recuento

Peso métrico de hello agrega métrica. No se debe establecer para una medida.

## <a name="min"></a>Min

Valor mínimo de hello agrega métrica. No se debe establecer para una medida.

## <a name="max"></a>max

Valor máximo de hello agrega métrica. No se debe establecer para una medida.

## <a name="standard-deviation"></a>Desviación estándar

Desviación estándar de hello agrega métrica. No se debe establecer para una medida.

## <a name="custom-properties"></a>Propiedades personalizadas

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo toouse [API de visión de la aplicación para eventos personalizados y las métricas](app-insights-api-custom-events-metrics.md#trackmetric).
- Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.
- Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.
