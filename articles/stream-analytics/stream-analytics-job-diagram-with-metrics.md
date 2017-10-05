---
title: "Depuración orientada a datos de Azure Stream Analytics mediante el diagrama de trabajo | Microsoft Docs"
description: "Solucione los problemas de los trabajos de Stream Analytics mediante el diagrama de trabajo y las métricas."
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
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="1fa5d-103">Depuración orientada a datos mediante el diagrama de trabajo</span><span class="sxs-lookup"><span data-stu-id="1fa5d-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="1fa5d-104">El diagrama de trabajo de la hoja **Supervisión** del portal de Azure puede ayudarle a visualizar su canalización de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="1fa5d-105">Muestra las entradas, las salidas y los pasos de consulta.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="1fa5d-106">Puede usar el diagrama de trabajo para examinar las métricas de cada paso y así aislar más rápidamente el origen de un problema cuando tenga que solucionarlo.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="1fa5d-107">Uso del diagrama de trabajo</span><span class="sxs-lookup"><span data-stu-id="1fa5d-107">Using the job diagram</span></span>

<span data-ttu-id="1fa5d-108">En el portal de Azure, mientras está en un trabajo de Stream Analytics, en **SOPORTE TÉCNICO Y SOLUCIÓN DE PROBLEMAS**, seleccione **Diagrama de trabajo**:</span><span class="sxs-lookup"><span data-stu-id="1fa5d-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagrama de trabajo con métricas: ubicación](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="1fa5d-110">Seleccione cada paso de consulta para ver la sección correspondiente en un panel de edición de consultas.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="1fa5d-111">Se muestra un gráfico de métricas para el paso en la sección inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![Diagrama de trabajo con métricas: trabajo básico](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="1fa5d-113">Para ver las particiones de la entrada de Azure Event Hubs, seleccione **. . .**</span><span class="sxs-lookup"><span data-stu-id="1fa5d-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="1fa5d-114">Aparece un menú contextual.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-114">A context menu appears.</span></span> <span data-ttu-id="1fa5d-115">También puede ver la fusión de entrada.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-115">You also can see the input merger.</span></span>

![Diagrama de trabajo con métricas: expandir partición](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="1fa5d-117">Para ver el gráfico de métricas para una sola partición, seleccione el nodo de la partición.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="1fa5d-118">Las métricas se muestran en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-118">The metrics are shown at the bottom of the page.</span></span>

![Diagrama de trabajo con métricas: más métricas](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="1fa5d-120">Para ver el gráfico de métricas de una fusión, seleccione el nodo de fusión.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="1fa5d-121">El gráfico siguiente muestra que no se quitó ni ajustó ningún evento.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-121">The following chart shows that no events were dropped or adjusted.</span></span>

![Diagrama de trabajo con métricas: cuadrícula](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="1fa5d-123">Para ver los detalles del valor de métrica y la hora, apunte al gráfico.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-123">To see the details of the metric value and time, point to the chart.</span></span>

![Diagrama de trabajo con métricas: mantener el mouse](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="1fa5d-125">Solución de problemas mediante métricas</span><span class="sxs-lookup"><span data-stu-id="1fa5d-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="1fa5d-126">La métrica **QueryLastProcessedTime** indica cuando un paso específico recibió datos.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="1fa5d-127">Si examina la topología, puede volver atrás desde el procesador de salida para ver qué paso no recibe datos.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="1fa5d-128">Si un paso no recibe datos, vaya al paso de consulta justo delante de él.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="1fa5d-129">Compruebe que el paso de consulta anterior tenga una ventana de tiempo, y que se le haya pasado suficiente tiempo para generar datos.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="1fa5d-130">(Observe que las ventanas de tiempo están ajustadas a la hora.)</span><span class="sxs-lookup"><span data-stu-id="1fa5d-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="1fa5d-131">Si el paso de consulta anterior es un procesador de entrada, use las métricas de entrada como ayuda para responder a las siguientes preguntas ayude a responder las siguientes preguntas dirigidas.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="1fa5d-132">Pueden ayudarle a determinar si un trabajo recibe datos de sus orígenes de entrada.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="1fa5d-133">Si la consulta está particionada, examine cada partición.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="1fa5d-134">¿Cuántos datos se están leyendo?</span><span class="sxs-lookup"><span data-stu-id="1fa5d-134">How much data is being read?</span></span>

*   <span data-ttu-id="1fa5d-135">**InputEventsSourcesTotal** es el número de unidades de datos leídas.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="1fa5d-136">Por ejemplo, el número de blobs.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="1fa5d-137">**InputEventsTotal** es el número de eventos leídos.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="1fa5d-138">Esta métrica está disponible por partición.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="1fa5d-139">**InputEventsInBytesTotal** es el número de bytes leídos.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="1fa5d-140">**InputEventsLastArrivalTime** se actualiza con el tiempo que está puesto en cola cada evento recibido.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="1fa5d-141">¿Avanza el tiempo?</span><span class="sxs-lookup"><span data-stu-id="1fa5d-141">Is time moving forward?</span></span> <span data-ttu-id="1fa5d-142">Si se leen eventos reales, es posible que no se emita la puntuación.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="1fa5d-143">**InputEventsLastPunctuationTime** indica cuando se emitió una puntuación para mantener el tiempo avanzando.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="1fa5d-144">El flujo de datos puede bloquearse si no se emite la puntuación.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="1fa5d-145">¿Hay errores en la entrada?</span><span class="sxs-lookup"><span data-stu-id="1fa5d-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="1fa5d-146">**InputEventsEventDataNullTotal** es el número de eventos que tienen datos nulos.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="1fa5d-147">**InputEventsSerializerErrorsTotal** es el número de eventos que no se pudieron deserializar correctamente.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="1fa5d-148">**InputEventsDegradedTotal** es el número de eventos que tuvieron un problema distinto al de la deserialización.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="1fa5d-149">¿Se van a descartar o ajustar los eventos?</span><span class="sxs-lookup"><span data-stu-id="1fa5d-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="1fa5d-150">**InputEventsEarlyTotal** es el número de eventos con una marca de tiempo de la aplicación antes del límite máximo.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="1fa5d-151">**InputEventsLateTotal** es el número de eventos con una marca de tiempo de la aplicación después del límite máximo.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="1fa5d-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** es el número de eventos descartados antes de la hora de inicio del trabajo.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="1fa5d-153">¿Estamos retrasados en la lectura de los datos?</span><span class="sxs-lookup"><span data-stu-id="1fa5d-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="1fa5d-154">**InputEventsSourcesBackloggedTotal** indica cuántos mensajes más es necesario leer para las entradas de Event Hubs y Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa5d-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="1fa5d-155">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="1fa5d-155">Get help</span></span>
<span data-ttu-id="1fa5d-156">Para obtener más ayuda, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1fa5d-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fa5d-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1fa5d-157">Next steps</span></span>
* [<span data-ttu-id="1fa5d-158">¿Qué es Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="1fa5d-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1fa5d-159">Introducción a Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fa5d-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1fa5d-160">Escalado de trabajos de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fa5d-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1fa5d-161">Referencia de lenguaje de consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fa5d-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1fa5d-162">Referencia de API de REST de administración de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fa5d-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
