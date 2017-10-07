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
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="14533-103">Depuración con el diagrama de trabajo de hello controladas por datos</span><span class="sxs-lookup"><span data-stu-id="14533-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="14533-104">diagrama de trabajo de Hello en hello **supervisión** hoja Hola portal de Azure puede ayudarle a visualizar la canalización de trabajo.</span><span class="sxs-lookup"><span data-stu-id="14533-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="14533-105">Muestra las entradas, las salidas y los pasos de consulta.</span><span class="sxs-lookup"><span data-stu-id="14533-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="14533-106">Hola trabajo diagrama tooexamine Hola métricas se pueden usar para cada paso, toomore aislar rápidamente el origen de Hola de un problema para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="14533-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="14533-107">Usar Hola trabajo diagrama</span><span class="sxs-lookup"><span data-stu-id="14533-107">Using hello job diagram</span></span>

<span data-ttu-id="14533-108">Hola portal de Azure, mientras se encuentre en un trabajo de análisis de transmisiones, en **soporte técnico y solución de problemas**, seleccione **diagrama de trabajo**:</span><span class="sxs-lookup"><span data-stu-id="14533-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagrama de trabajo con métricas: ubicación](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="14533-110">Seleccione cada sección consulta paso toosee Hola correspondiente en un panel de edición de consultas.</span><span class="sxs-lookup"><span data-stu-id="14533-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="14533-111">Se muestra un gráfico de métricas para el paso de hello en un página de hello del panel inferior.</span><span class="sxs-lookup"><span data-stu-id="14533-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagrama de trabajo con métricas: trabajo básico](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="14533-113">Seleccione las particiones de hello toosee de entrada de los centros de eventos de Azure de hello, **...**</span><span class="sxs-lookup"><span data-stu-id="14533-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="14533-114">Aparece un menú contextual.</span><span class="sxs-lookup"><span data-stu-id="14533-114">A context menu appears.</span></span> <span data-ttu-id="14533-115">También puede ver la fusión de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="14533-115">You also can see hello input merger.</span></span>

![Diagrama de trabajo con métricas: expandir partición](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="14533-117">gráfico de métricas de Hola de toosee para solo una sola partición, nodo de la partición de hello seleccione.</span><span class="sxs-lookup"><span data-stu-id="14533-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="14533-118">se muestran las métricas de Hello final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="14533-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagrama de trabajo con métricas: más métricas](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="14533-120">gráfico de métricas de hello toosee para una fusión, nodo de fusión de hello select.</span><span class="sxs-lookup"><span data-stu-id="14533-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="14533-121">Hola tabla siguiente se muestra que se quitaron o se ajusta ningún evento.</span><span class="sxs-lookup"><span data-stu-id="14533-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagrama de trabajo con métricas: cuadrícula](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="14533-123">detalles de hello toosee de valor de métrica de Hola y la hora, punto toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="14533-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diagrama de trabajo con métricas: mantener el mouse](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="14533-125">Solución de problemas mediante métricas</span><span class="sxs-lookup"><span data-stu-id="14533-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="14533-126">Hola **QueryLastProcessedTime** métrica indica cuando un paso concreto recibe datos.</span><span class="sxs-lookup"><span data-stu-id="14533-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="14533-127">Examinando topología hello, pueden trabajar hacia atrás desde toosee de procesador de salida de hello paso que no está recibiendo datos.</span><span class="sxs-lookup"><span data-stu-id="14533-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="14533-128">Si un paso no está obteniendo datos, vaya toohello paso de consulta antes de que.</span><span class="sxs-lookup"><span data-stu-id="14533-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="14533-129">Compruebe si el paso de consulta anterior hello tiene un período de tiempo, y si ha transcurrido tiempo suficiente para los datos de toooutput.</span><span class="sxs-lookup"><span data-stu-id="14533-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="14533-130">(Observe que el momento windows están ajustados toohello hora).</span><span class="sxs-lookup"><span data-stu-id="14533-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="14533-131">Si hello paso de consulta anterior es un procesador de entrada, utilice Hola de respuesta de toohelp hello las métricas de entrada siguientes preguntas de destino.</span><span class="sxs-lookup"><span data-stu-id="14533-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="14533-132">Pueden ayudarle a determinar si un trabajo recibe datos de sus orígenes de entrada.</span><span class="sxs-lookup"><span data-stu-id="14533-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="14533-133">Si consulta hello tiene particiones, examine cada partición.</span><span class="sxs-lookup"><span data-stu-id="14533-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="14533-134">¿Cuántos datos se están leyendo?</span><span class="sxs-lookup"><span data-stu-id="14533-134">How much data is being read?</span></span>

*   <span data-ttu-id="14533-135">**InputEventsSourcesTotal** es Hola número de unidades de datos de lectura.</span><span class="sxs-lookup"><span data-stu-id="14533-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="14533-136">Por ejemplo, número de Hola de blobs.</span><span class="sxs-lookup"><span data-stu-id="14533-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="14533-137">**InputEventsTotal** es Hola número de eventos de lectura.</span><span class="sxs-lookup"><span data-stu-id="14533-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="14533-138">Esta métrica está disponible por partición.</span><span class="sxs-lookup"><span data-stu-id="14533-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="14533-139">**InputEventsInBytesTotal** es Hola número de bytes leídos.</span><span class="sxs-lookup"><span data-stu-id="14533-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="14533-140">**InputEventsLastArrivalTime** se actualiza con el tiempo que está puesto en cola cada evento recibido.</span><span class="sxs-lookup"><span data-stu-id="14533-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="14533-141">¿Avanza el tiempo?</span><span class="sxs-lookup"><span data-stu-id="14533-141">Is time moving forward?</span></span> <span data-ttu-id="14533-142">Si se leen eventos reales, es posible que no se emita la puntuación.</span><span class="sxs-lookup"><span data-stu-id="14533-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="14533-143">**InputEventsLastPunctuationTime** indica cuando se emitió una puntuación tookeep tiempo mover hacia delante.</span><span class="sxs-lookup"><span data-stu-id="14533-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="14533-144">El flujo de datos puede bloquearse si no se emite la puntuación.</span><span class="sxs-lookup"><span data-stu-id="14533-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="14533-145">¿Hay algún error en la entrada de hello?</span><span class="sxs-lookup"><span data-stu-id="14533-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="14533-146">**InputEventsEventDataNullTotal** es el número de eventos que tienen datos nulos.</span><span class="sxs-lookup"><span data-stu-id="14533-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="14533-147">**InputEventsSerializerErrorsTotal** es el número de eventos que no se pudieron deserializar correctamente.</span><span class="sxs-lookup"><span data-stu-id="14533-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="14533-148">**InputEventsDegradedTotal** es el número de eventos que tuvieron un problema distinto al de la deserialización.</span><span class="sxs-lookup"><span data-stu-id="14533-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="14533-149">¿Se van a descartar o ajustar los eventos?</span><span class="sxs-lookup"><span data-stu-id="14533-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="14533-150">**InputEventsEarlyTotal** es Hola número de eventos que tienen una marca de tiempo de aplicación antes de límite máximo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14533-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="14533-151">**InputEventsLateTotal** es Hola número de eventos que tienen una marca de tiempo de aplicación después de la marca de agua alta Hola.</span><span class="sxs-lookup"><span data-stu-id="14533-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="14533-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** es quitado antes de tiempo de inicio del trabajo de hello número de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="14533-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="14533-153">¿Estamos retrasados en la lectura de los datos?</span><span class="sxs-lookup"><span data-stu-id="14533-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="14533-154">**InputEventsSourcesBackloggedTotal** indica cuántos mensajes más necesitan toobe de lectura para las entradas de centro de IoT de Azure y centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="14533-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="14533-155">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="14533-155">Get help</span></span>
<span data-ttu-id="14533-156">Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="14533-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="14533-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14533-157">Next steps</span></span>
* [<span data-ttu-id="14533-158">Introducción tooStream análisis</span><span class="sxs-lookup"><span data-stu-id="14533-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="14533-159">Introducción a Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14533-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="14533-160">Escalado de trabajos de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14533-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="14533-161">Referencia de lenguaje de consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14533-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="14533-162">Referencia de API de REST de administración de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14533-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
