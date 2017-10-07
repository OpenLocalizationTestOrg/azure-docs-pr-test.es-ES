---
title: "aaa análisis de transmisiones de Azure controladas por datos depurar mediante el diagrama de trabajo de hello | Documentos de Microsoft"
description: "Solucionar problemas de su trabajo de análisis de transmisiones mediante el uso de las métricas y diagrama de trabajo de Hola."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Depuración con el diagrama de trabajo de hello controladas por datos

diagrama de trabajo de Hello en hello **supervisión** hoja Hola portal de Azure puede ayudarle a visualizar la canalización de trabajo. Muestra las entradas, las salidas y los pasos de consulta. Hola trabajo diagrama tooexamine Hola métricas se pueden usar para cada paso, toomore aislar rápidamente el origen de Hola de un problema para solucionar problemas.

## <a name="using-hello-job-diagram"></a>Usar Hola trabajo diagrama

Hola portal de Azure, mientras se encuentre en un trabajo de análisis de transmisiones, en **soporte técnico y solución de problemas**, seleccione **diagrama de trabajo**:

![Diagrama de trabajo con métricas: ubicación](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Seleccione cada sección consulta paso toosee Hola correspondiente en un panel de edición de consultas. Se muestra un gráfico de métricas para el paso de hello en un página de hello del panel inferior.

![Diagrama de trabajo con métricas: trabajo básico](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

Seleccione las particiones de hello toosee de entrada de los centros de eventos de Azure de hello, **...** Aparece un menú contextual. También puede ver la fusión de entrada de Hola.

![Diagrama de trabajo con métricas: expandir partición](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

gráfico de métricas de Hola de toosee para solo una sola partición, nodo de la partición de hello seleccione. se muestran las métricas de Hello final Hola de página Hola.

![Diagrama de trabajo con métricas: más métricas](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

gráfico de métricas de hello toosee para una fusión, nodo de fusión de hello select. Hola tabla siguiente se muestra que se quitaron o se ajusta ningún evento.

![Diagrama de trabajo con métricas: cuadrícula](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

detalles de hello toosee de valor de métrica de Hola y la hora, punto toohello gráfico.

![Diagrama de trabajo con métricas: mantener el mouse](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Solución de problemas mediante métricas

Hola **QueryLastProcessedTime** métrica indica cuando un paso concreto recibe datos. Examinando topología hello, pueden trabajar hacia atrás desde toosee de procesador de salida de hello paso que no está recibiendo datos. Si un paso no está obteniendo datos, vaya toohello paso de consulta antes de que. Compruebe si el paso de consulta anterior hello tiene un período de tiempo, y si ha transcurrido tiempo suficiente para los datos de toooutput. (Observe que el momento windows están ajustados toohello hora).
 
Si hello paso de consulta anterior es un procesador de entrada, utilice Hola de respuesta de toohelp hello las métricas de entrada siguientes preguntas de destino. Pueden ayudarle a determinar si un trabajo recibe datos de sus orígenes de entrada. Si consulta hello tiene particiones, examine cada partición.
 
### <a name="how-much-data-is-being-read"></a>¿Cuántos datos se están leyendo?

*   **InputEventsSourcesTotal** es Hola número de unidades de datos de lectura. Por ejemplo, número de Hola de blobs.
*   **InputEventsTotal** es Hola número de eventos de lectura. Esta métrica está disponible por partición.
*   **InputEventsInBytesTotal** es Hola número de bytes leídos.
*   **InputEventsLastArrivalTime** se actualiza con el tiempo que está puesto en cola cada evento recibido.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>¿Avanza el tiempo? Si se leen eventos reales, es posible que no se emita la puntuación.

*   **InputEventsLastPunctuationTime** indica cuando se emitió una puntuación tookeep tiempo mover hacia delante. El flujo de datos puede bloquearse si no se emite la puntuación.
 
### <a name="are-there-any-errors-in-hello-input"></a>¿Hay algún error en la entrada de hello?

*   **InputEventsEventDataNullTotal** es el número de eventos que tienen datos nulos.
*   **InputEventsSerializerErrorsTotal** es el número de eventos que no se pudieron deserializar correctamente.
*   **InputEventsDegradedTotal** es el número de eventos que tuvieron un problema distinto al de la deserialización.
 
### <a name="are-events-being-dropped-or-adjusted"></a>¿Se van a descartar o ajustar los eventos?

*   **InputEventsEarlyTotal** es Hola número de eventos que tienen una marca de tiempo de aplicación antes de límite máximo de Hola.
*   **InputEventsLateTotal** es Hola número de eventos que tienen una marca de tiempo de aplicación después de la marca de agua alta Hola.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** es quitado antes de tiempo de inicio del trabajo de hello número de eventos de Hola.
 
### <a name="are-we-falling-behind-in-reading-data"></a>¿Estamos retrasados en la lectura de los datos?

*   **InputEventsSourcesBackloggedTotal** indica cuántos mensajes más necesitan toobe de lectura para las entradas de centro de IoT de Azure y centros de eventos.


## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooStream análisis](stream-analytics-introduction.md)
* [Introducción a Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalado de trabajos de Stream Analytics](stream-analytics-scale-jobs.md)
* [Referencia de lenguaje de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
