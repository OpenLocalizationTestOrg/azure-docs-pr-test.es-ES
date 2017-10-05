---
title: "Azure Stream Analytics: optimización del trabajo para usar unidades de streaming de forma efectiva | Microsoft Docs"
description: Procedimientos de consulta recomendados para escalado y rendimiento en Azure Stream Analytics.
keywords: unidad de streaming, rendimiento de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 1441a5df4fd92abf85763ca9a1512503b1a0da56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-job-to-use-streaming-units-efficiently"></a><span data-ttu-id="c968d-104">Optimización del trabajo para usar unidades de streaming de forma eficaz</span><span class="sxs-lookup"><span data-stu-id="c968d-104">Optimize your job to use Streaming Units efficiently</span></span>

<span data-ttu-id="c968d-105">Azure Stream Analytics agrega el "peso" de rendimiento de ejecutar un trabajo en unidades de streaming (SU).</span><span class="sxs-lookup"><span data-stu-id="c968d-105">Azure Stream Analytics aggregates the performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="c968d-106">Las SU representan los recursos informáticos que se usan para ejecutar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="c968d-106">SUs represent the computing resources that are consumed to execute a job.</span></span> <span data-ttu-id="c968d-107">Las SU proporcionan una forma de describir la capacidad de procesamiento del evento relativo en función de una medida que combina la CPU, la memoria y las tasas de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="c968d-107">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="c968d-108">Esta capacidad le permite centrarse en la lógica de consulta y elimina la necesidad de conocer las consideraciones de rendimiento de los niveles de almacenamiento, de asignar memoria para su trabajo manualmente y de aproximar el número de núcleos de CPU para ejecutar su trabajo de manera oportuna.</span><span class="sxs-lookup"><span data-stu-id="c968d-108">This capacity lets you focus on the query logic and removes you from needing to know storage tier performance considerations, allocate memory for your job manually, and approximate the CPU core-count needed to run your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="c968d-109">¿Cuántas SU son necesarias para un trabajo?</span><span class="sxs-lookup"><span data-stu-id="c968d-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="c968d-110">La elección del número de SU necesarias para un trabajo determinado depende de la configuración de particiones de las entradas y de la consulta definida dentro del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c968d-110">Choosing the number of required SUs for a particular job depends on the partition configuration for the inputs and the query that's defined within the job.</span></span> <span data-ttu-id="c968d-111">La hoja **Escala** le permite establecer el número correcto de SU.</span><span class="sxs-lookup"><span data-stu-id="c968d-111">The **Scale** blade allows you to set the right number of SUs.</span></span> <span data-ttu-id="c968d-112">Es recomendable asignar más unidades de streaming de las necesarias.</span><span class="sxs-lookup"><span data-stu-id="c968d-112">It is a best practice to allocate more SUs than needed.</span></span> <span data-ttu-id="c968d-113">El motor de procesamiento de Stream Analytics se optimiza para la latencia y el rendimiento, a costa de asignar memoria adicional.</span><span class="sxs-lookup"><span data-stu-id="c968d-113">The Stream Analytics processing engine optimizes for latency and throughput at the cost of allocating additional memory.</span></span>

<span data-ttu-id="c968d-114">En general, el procedimiento recomendado es comenzar con 6 SU para consultas que no usen *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="c968d-114">In general, the best practice is to start with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="c968d-115">Luego, determine el punto favorable mediante un método de prueba y error en el que modifica el número de SU después de pasar las cantidades de datos representativas y examinar la métrica de porcentaje de uso de SU.</span><span class="sxs-lookup"><span data-stu-id="c968d-115">Then determine the sweet spot by using a trial and error method in which you modify the number of SUs after you pass representative amounts of data and examine the SU %Utilization metric.</span></span>

<span data-ttu-id="c968d-116">Azure Stream Analytics mantiene los eventos en una ventana llamada "búfer de reordenación" antes de comenzar cualquier procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c968d-116">Azure Stream Analytics keeps events in a window called the “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="c968d-117">Los eventos se ordenan dentro de la ventana de reordenación por hora y las operaciones posteriores se realizan en los eventos ordenados temporalmente.</span><span class="sxs-lookup"><span data-stu-id="c968d-117">Events are sorted within the reorder window by time, and subsequent operations are performed on the temporally sorted events.</span></span> <span data-ttu-id="c968d-118">La reordenación de eventos por hora garantiza que el operador tiene visibilidad sobre los tres eventos en el período de tiempo estipulado.</span><span class="sxs-lookup"><span data-stu-id="c968d-118">Reordering events by time ensures that the operator has visibility into all the events in the stipulated timeframe.</span></span> <span data-ttu-id="c968d-119">También permite al operador realizar el procesamiento de requisitos y generar una salida.</span><span class="sxs-lookup"><span data-stu-id="c968d-119">It also lets the operator perform the requisite processing and produce an output.</span></span> <span data-ttu-id="c968d-120">Un efecto secundario de este mecanismo es que el procesamiento se retrasa el tiempo que dura la ventana de reorganización.</span><span class="sxs-lookup"><span data-stu-id="c968d-120">A side effect of this mechanism is that processing is delayed by the duration of the reorder window.</span></span> <span data-ttu-id="c968d-121">La superficie de memoria del trabajo (que afecta al consumo de la unidad de streaming) es una función del tamaño de esta ventana de reordenación y el número de eventos que contiene.</span><span class="sxs-lookup"><span data-stu-id="c968d-121">The memory footprint of the job (which affects SU consumption) is a function of the size of this reorder window and the number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="c968d-122">Cuando el número de lectores cambia durante las actualizaciones de trabajos, se escriben advertencias transitorias en registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="c968d-122">When the number of readers changes during job upgrades, transient warnings are written to audit logs.</span></span> <span data-ttu-id="c968d-123">Los trabajos de Stream Analytics se recuperan automáticamente de estos problemas transitorios.</span><span class="sxs-lookup"><span data-stu-id="c968d-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="c968d-124">Causas comunes de memoria alta por el uso elevado de SU para la ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="c968d-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="c968d-125">Alta cardinalidad para GROUP BY</span><span class="sxs-lookup"><span data-stu-id="c968d-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="c968d-126">La cardinalidad de los eventos de entrada determina el uso de memoria para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c968d-126">The cardinality of incoming events dictates memory usage for the job.</span></span>

<span data-ttu-id="c968d-127">Por ejemplo, en `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, el número asociado con **clustered** es la cardinalidad de la consulta.</span><span class="sxs-lookup"><span data-stu-id="c968d-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, the number associated with **clustered** is the cardinality of the query.</span></span>

<span data-ttu-id="c968d-128">Para mitigar los problemas ocasionados por una cardinalidad alta, escale horizontalmente la consulta aumentando las particiones con **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="c968d-128">To mitigate issues that are caused by high cardinality, scale out the query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="c968d-129">Aquí, el número de *clustered* es la cardinalidad de GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="c968d-129">The number of *clustered* is the cardinality of GROUP BY here.</span></span>

<span data-ttu-id="c968d-130">Una vez que la consulta está particionada, se extiende por varios nodos.</span><span class="sxs-lookup"><span data-stu-id="c968d-130">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="c968d-131">Como resultado, el número de eventos que entra en cada nodo se reduce, lo que a su vez disminuye el tamaño del búfer de reordenación.</span><span class="sxs-lookup"><span data-stu-id="c968d-131">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> <span data-ttu-id="c968d-132">También debe particionar las particiones de centro de eventos mediante partitionid.</span><span class="sxs-lookup"><span data-stu-id="c968d-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="c968d-133">Recuento alto de eventos no coincidentes para JOIN</span><span class="sxs-lookup"><span data-stu-id="c968d-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="c968d-134">El número de eventos no coincidentes en JOIN afecta a la utilización de memoria de la consulta.</span><span class="sxs-lookup"><span data-stu-id="c968d-134">The number of unmatched events in a JOIN affects the memory utilization of the query.</span></span> <span data-ttu-id="c968d-135">Por ejemplo, imagine una consulta que busca encontrar el número de impresiones de anuncios que generan clics:</span><span class="sxs-lookup"><span data-stu-id="c968d-135">For example, take a query that is looking to find the number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="c968d-136">En este escenario, es posible que se muestren muchos anuncios y se generen pocos clics.</span><span class="sxs-lookup"><span data-stu-id="c968d-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="c968d-137">Un resultado de este tipo podría requerir que el trabajo mantuviera todos los eventos dentro de la ventana de tiempo.</span><span class="sxs-lookup"><span data-stu-id="c968d-137">Such a result would require the job to keep all the events within the time window.</span></span> <span data-ttu-id="c968d-138">La cantidad de memoria consumida es proporcional al tamaño de ventana y la tasa de eventos.</span><span class="sxs-lookup"><span data-stu-id="c968d-138">The amount of memory consumed is proportional to the window size and event rate.</span></span> 

<span data-ttu-id="c968d-139">Para mitigar esta situación, escale horizontalmente la consulta aumentando las particiones mediante PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="c968d-139">To mitigate this situation, scale out the query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="c968d-140">Después de particionar la consulta, se distribuye entre varios nodos de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c968d-140">After the query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="c968d-141">Como resultado, el número de eventos que entra en cada nodo se reduce, lo que a su vez disminuye el tamaño del búfer de reordenación.</span><span class="sxs-lookup"><span data-stu-id="c968d-141">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="c968d-142">Gran número de eventos desordenados</span><span class="sxs-lookup"><span data-stu-id="c968d-142">Large number of out of order events</span></span> 

<span data-ttu-id="c968d-143">Un gran número de eventos desordenados en una ventana de tiempo grande hace que el tamaño del "búfer de reordenación" sea mayor.</span><span class="sxs-lookup"><span data-stu-id="c968d-143">A large number of out of order events within a large time window causes the size of the "reorder buffer" to be larger.</span></span> <span data-ttu-id="c968d-144">Para mitigar esta situación, escale la consulta aumentando las particiones mediante PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="c968d-144">To mitigate this situation, scale the query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="c968d-145">Una vez que la consulta está particionada, se extiende por varios nodos.</span><span class="sxs-lookup"><span data-stu-id="c968d-145">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="c968d-146">Como resultado, el número de eventos que entra en cada nodo se reduce, lo que a su vez disminuye el tamaño del búfer de reordenación.</span><span class="sxs-lookup"><span data-stu-id="c968d-146">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="c968d-147">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="c968d-147">Get help</span></span>
<span data-ttu-id="c968d-148">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c968d-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c968d-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c968d-149">Next steps</span></span>
* [<span data-ttu-id="c968d-150">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c968d-150">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c968d-151">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c968d-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c968d-152">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="c968d-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c968d-153">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c968d-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c968d-154">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c968d-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
