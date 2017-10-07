---
title: "Supervisión de trabajo de análisis de transmisiones de aaaUnderstanding | Documentos de Microsoft"
description: "Descripción de la supervisión del trabajo de Análisis de transmisiones"
keywords: "supervisión de consultas"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Comprender la supervisión de trabajo de análisis de transmisiones y cómo toomonitor consultas

## <a name="introduction-hello-monitor-page"></a>Introducción: página Hola monitor
Hola ambos expuesta métricas de rendimiento clave que se pueden toomonitor usado y solucionar problemas de rendimiento de la consulta y el trabajo de portal de Azure. toosee estas métricas, examinar está interesado en Ver hello de vista y las métricas para el trabajo de análisis de flujo de toohello **supervisión** sección en la página de información general de Hola.  

![Vínculo de supervisión](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

ventana Hello aparecerán como se muestra:

![Panel de supervisión de trabajos](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Métricas disponibles para Análisis de transmisiones
| Métrica                 | Definición                               |
| ---------------------- | ---------------------------------------- |
| SU % uso       | uso de Hola de hello unidades de transmisión por secuencias asignados tooa trabajo Hola de ficha escala del trabajo de Hola. Si este indicador llega o supera el 80 %, existe una gran probabilidad de que el procesamiento de eventos se retrase o deje de avanzar. |
| Eventos de entrada           | Cantidad de datos recibidos por el trabajo de análisis de transmisiones de hello, en número de eventos. Esto puede ser usado toovalidate que se envían eventos de origen de entrada de toohello. |
| Eventos de salida          | Cantidad de datos enviados por hello análisis de transmisiones trabajo toohello destino de salida, en número de eventos. |
| Eventos que no funcionan    | Número de eventos recibidos fuera de servicio que se anularon o tiene una marca de tiempo ajustada, basada en hello directiva de orden de eventos. Esto se puede ver afectado por la configuración de Hola de configuración de la ventana de tolerancia de fuera de lugar Hola. |
| Errores de conversión de datos | Número de errores de conversión de datos que produce un trabajo de Análisis de transmisiones. |
| Errores de tiempo de ejecución         | número total de Hola de errores que se producen durante la ejecución de un trabajo de análisis de transmisiones. |
| Eventos de entrada retrasada      | Número de eventos que llegan tarde desde el origen de Hola que ya se han eliminado o su marca de tiempo se ha ajustado, en función de la configuración de directiva de orden de eventos de Hola de tiempo de ejecución de tolerancia de llegada tardía Hola. |
| Solicitudes de función      | Número de llamadas toohello función de aprendizaje automático de Azure (si existe). |
| Solicitudes de función con errores | Número de llamadas a la función Azure Machine Learning con error (si corresponde). |
| Eventos de función        | Número de eventos enviados toohello función de aprendizaje automático de Azure (si existe). |
| Bytes del evento de entrada      | Cantidad de datos recibidos por trabajo de análisis de transmisiones de hello, en bytes. Esto puede ser usado toovalidate que se envían eventos de origen de entrada de toohello. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Personalizar supervisión en el portal de Azure Hola
Puede ajustar el tipo de gráfico de métricas que se muestran, Hola y el intervalo en la configuración de hello Editar gráfico de tiempo. Para obtener más información, consulte [cómo tooCustomize supervisión](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Escala de tiempo de supervisión de consultas](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

