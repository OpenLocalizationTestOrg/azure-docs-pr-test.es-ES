---
title: "rendimiento de tooincrease de trabajos de análisis de transmisiones de aaaScale | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale los trabajos de análisis de transmisiones por configurar particiones de entrada, la definición de la consulta de hello para la optimización y la configuración del trabajo unidades de streaming."
keywords: "datos de streaming, procesamiento de datos de streaming, optimización del análisis"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="c0536-104">Rendimiento de procesamiento de datos de escala análisis de transmisiones de Azure trabajos tooincrease stream</span><span class="sxs-lookup"><span data-stu-id="c0536-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="c0536-105">Este artículo muestra cómo tootune un análisis de transmisiones de consultar el rendimiento tooincrease para trabajos de análisis de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="c0536-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="c0536-106">Obtener información sobre cómo trabajos tooscale análisis de transmisiones mediante la configuración de particiones de entrada, definición de la consulta de análisis de optimización hello y calcular y la configuración del trabajo *unidades de streaming* (SUs).</span><span class="sxs-lookup"><span data-stu-id="c0536-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="c0536-107">¿Qué partes de Hola de un trabajo de análisis de transmisiones?</span><span class="sxs-lookup"><span data-stu-id="c0536-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="c0536-108">Una definición de trabajo de Análisis de transmisiones incluye entradas, una consulta y la salida.</span><span class="sxs-lookup"><span data-stu-id="c0536-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="c0536-109">Las entradas son donde trabajo Hola lee el flujo de datos de Hola de.</span><span class="sxs-lookup"><span data-stu-id="c0536-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="c0536-110">consulta Hello es flujo de entrada de datos de hello tootransform usado, y salida de hello es donde trabajo Hola envía los resultados del trabajo de Hola a.</span><span class="sxs-lookup"><span data-stu-id="c0536-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="c0536-111">Un trabajo requiere al menos un origen de entrada de streaming de datos.</span><span class="sxs-lookup"><span data-stu-id="c0536-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="c0536-112">Hello origen de entrada de flujo de datos puede almacenarse en un centro de eventos de Azure o en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0536-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="c0536-113">Para obtener más información, consulte [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md) y [Introducción al uso de análisis de transmisiones de Azure](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="c0536-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="c0536-114">Particiones en Event Hubs y Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c0536-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="c0536-115">Ajuste de escala en un trabajo de análisis de transmisiones aprovecha las ventajas de las particiones de hello entrada o salida.</span><span class="sxs-lookup"><span data-stu-id="c0536-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="c0536-116">La creación de particiones permite dividir los datos en subconjuntos en función de una clave de partición.</span><span class="sxs-lookup"><span data-stu-id="c0536-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="c0536-117">Un proceso que consume datos de hello (por ejemplo, un trabajo de análisis de transmisión por secuencias) puede consumir y escribir diferentes particiones en paralelo, lo que aumenta el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c0536-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="c0536-118">Si trabaja con Stream Analytics, puede aprovechar las ventajas de las particiones en Event Hubs y Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c0536-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="c0536-119">Para obtener más información acerca de las particiones, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c0536-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="c0536-120">Información general de las características de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c0536-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="c0536-121">Creación de particiones de datos</span><span class="sxs-lookup"><span data-stu-id="c0536-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="c0536-122">Unidades de streaming (SU)</span><span class="sxs-lookup"><span data-stu-id="c0536-122">Streaming units (SUs)</span></span>
<span data-ttu-id="c0536-123">Transmisión por secuencias unidades (SUs) representan Hola recursos y capacidad de ejecución que son necesarios en orden tooexecute un trabajo de análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0536-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="c0536-124">SUs proporcionan una manera toodescribe Hola relativa de eventos basándose en una medición mezclada de CPU, memoria, la capacidad de procesamiento y se leen y escriben las tasas.</span><span class="sxs-lookup"><span data-stu-id="c0536-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="c0536-125">Cada SU corresponde tooroughly 1 MB/segundo de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c0536-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="c0536-126">Elegir SUs cuántos son necesarios para un trabajo determinado depende en configuración de la partición de Hola para las entradas de Hola y de consulta de hello definida para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="c0536-127">Puede seleccionar una cuota de tooyour en SUs para un trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0536-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="c0536-128">De forma predeterminada, cada suscripción de Azure tiene una cuota de seguridad de SUs too50 para todos los trabajos de análisis de hello en una región específica.</span><span class="sxs-lookup"><span data-stu-id="c0536-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="c0536-129">tooincrease SUs para las suscripciones más allá de esta cuota, póngase en contacto con [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c0536-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="c0536-130">Los valores válidos para unidades de streaming por trabajo son 1, 3, 6 y más en incrementos de 6.</span><span class="sxs-lookup"><span data-stu-id="c0536-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="c0536-131">Trabajos embarazosamente paralelos</span><span class="sxs-lookup"><span data-stu-id="c0536-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="c0536-132">Un *embarazosamente paralelas* trabajo es el escenario más escalable Hola tenemos en análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0536-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="c0536-133">Se conecta a una partición de la instancia de entrada tooone Hola de partición de tooone Hola consulta de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c0536-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="c0536-134">Este paralelismo tiene Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="c0536-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="c0536-135">Si la lógica de la consulta depende de hello misma clave que se va a procesar por hello misma consulta instancia, debe asegurarse de que los eventos de hello van toohello misma partición de los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="c0536-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="c0536-136">Los centros de eventos, esto significa que los datos de eventos de hello deben tener hello **PartitionKey** valor establecido.</span><span class="sxs-lookup"><span data-stu-id="c0536-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="c0536-137">También puede usar remitentes con particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="c0536-138">Para el almacenamiento de blobs, esto significa que se envían eventos de hello toohello carpeta de la misma partición.</span><span class="sxs-lookup"><span data-stu-id="c0536-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="c0536-139">Si la lógica de la consulta no requiere Hola misma clave toobe procesado por hello misma consulta instancia, puede pasar por alto este requisito.</span><span class="sxs-lookup"><span data-stu-id="c0536-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="c0536-140">Un ejemplo de esta lógica sería una sencilla consulta select-project-filter.</span><span class="sxs-lookup"><span data-stu-id="c0536-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="c0536-141">Una vez que se distribuyen los datos de hello en lado de entrada de hello, debe asegurarse de que la consulta tiene particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="c0536-142">Para ello, deberá toouse **Partition By** en todos los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="c0536-143">Se permiten varios pasos, pero todas ellas deben tener particiones por hello misma clave.</span><span class="sxs-lookup"><span data-stu-id="c0536-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="c0536-144">Actualmente, se debe establecer Hola particiones clave demasiado**PartitionId** en orden para hello trabajo toobe totalmente paralela.</span><span class="sxs-lookup"><span data-stu-id="c0536-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="c0536-145">Solo Event Hubs y Blob Storage admiten en este momento salidas con particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="c0536-146">Para la salida del concentrador de eventos, debe configurar toobe clave de partición de hello **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="c0536-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="c0536-147">Para la salida de almacenamiento de blobs, no tiene toodo nada.</span><span class="sxs-lookup"><span data-stu-id="c0536-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="c0536-148">número de Hola de particiones de entrada debe ser igual a número Hola de particiones de salida.</span><span class="sxs-lookup"><span data-stu-id="c0536-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="c0536-149">La salida de Blob Storage no admite en este momento la creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="c0536-150">Pero no importa, porque hereda Hola esquema de consulta de nivel superior de Hola de particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="c0536-151">Vea ejemplos de valores de partición que permiten un trabajo totalmente paralelo:</span><span class="sxs-lookup"><span data-stu-id="c0536-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="c0536-152">Ocho particiones de entrada de Event Hubs y ocho particiones de salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c0536-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="c0536-153">Ocho particiones de entrada de Event Hubs y salida de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="c0536-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="c0536-154">Ocho particiones de entrada de Blob Storage y salida de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="c0536-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="c0536-155">Ocho particiones de entrada de Blob Storage y ocho particiones de salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c0536-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="c0536-156">Hello las secciones siguientes describen algunos escenarios de ejemplo que son embarazosamente paralelas.</span><span class="sxs-lookup"><span data-stu-id="c0536-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="c0536-157">Consulta sencilla</span><span class="sxs-lookup"><span data-stu-id="c0536-157">Simple query</span></span>

* <span data-ttu-id="c0536-158">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c0536-159">Salida: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="c0536-160">Consulta:</span><span class="sxs-lookup"><span data-stu-id="c0536-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="c0536-161">Esta consulta es un filtro sencillo.</span><span class="sxs-lookup"><span data-stu-id="c0536-161">This query is a simple filter.</span></span> <span data-ttu-id="c0536-162">Por lo tanto, no es necesario tooworry acerca de las particiones de entrada de Hola que se están enviando toohello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="c0536-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="c0536-163">Tenga en cuenta que consultan Hola incluye **partición por PartitionId**, por lo que cumple el requisito #2 de antes.</span><span class="sxs-lookup"><span data-stu-id="c0536-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="c0536-164">Para la salida de hello, necesitamos salida del concentrador de eventos tooconfigure hello en el conjunto de claves de la partición de Hola de hello trabajo toohave demasiado**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="c0536-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="c0536-165">Una última comprobación es toomake asegurarse de que el número de Hola de particiones de entrada es igual toohello número de particiones de salida.</span><span class="sxs-lookup"><span data-stu-id="c0536-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="c0536-166">Consulta con una clave de agrupación</span><span class="sxs-lookup"><span data-stu-id="c0536-166">Query with a grouping key</span></span>

* <span data-ttu-id="c0536-167">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c0536-168">Salida: Blob Storage</span><span class="sxs-lookup"><span data-stu-id="c0536-168">Output: Blob storage</span></span>

<span data-ttu-id="c0536-169">Consulta:</span><span class="sxs-lookup"><span data-stu-id="c0536-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c0536-170">Esta consulta tiene una clave de agrupación.</span><span class="sxs-lookup"><span data-stu-id="c0536-170">This query has a grouping key.</span></span> <span data-ttu-id="c0536-171">Por lo tanto, Hola mismo toobe necesidades clave procesado por hello misma consulta instancias, lo que significa que los eventos se deben enviar toohello concentrador de eventos de manera con particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="c0536-172">¿Pero qué clave debe usarse?</span><span class="sxs-lookup"><span data-stu-id="c0536-172">But which key should be used?</span></span> <span data-ttu-id="c0536-173">**PartitionId** es un concepto de lógica de trabajos.</span><span class="sxs-lookup"><span data-stu-id="c0536-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="c0536-174">clave Hola nos preocupamos por realmente es **TollBoothId**, tan Hola **PartitionKey** debe ser el valor de los datos de evento de hello **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="c0536-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="c0536-175">Para ello en la consulta de hello estableciendo **Partition By** demasiado**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="c0536-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="c0536-176">Puesto que la salida de hello es el almacenamiento de blobs, no es necesario tooworry acerca de cómo configurar un valor de clave de partición, según el requisito #4.</span><span class="sxs-lookup"><span data-stu-id="c0536-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="c0536-177">Consulta de varios pasos con una clave de agrupación</span><span class="sxs-lookup"><span data-stu-id="c0536-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="c0536-178">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c0536-179">Salida: instancia de Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="c0536-180">Consulta:</span><span class="sxs-lookup"><span data-stu-id="c0536-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c0536-181">Esta consulta tiene una clave de agrupación, Hola así mismo toobe necesidades clave procesado por hello misma instancia de consulta.</span><span class="sxs-lookup"><span data-stu-id="c0536-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="c0536-182">Podemos usar Hola misma estrategia como en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="c0536-183">En este caso, la consulta de hello tiene varios pasos.</span><span class="sxs-lookup"><span data-stu-id="c0536-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="c0536-184">¿Cada paso tiene **Partition By PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="c0536-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="c0536-185">Sí, por lo que la consulta de hello cumple el requisito #3.</span><span class="sxs-lookup"><span data-stu-id="c0536-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="c0536-186">Para la salida de hello, necesitamos clave de partición de hello tooset demasiado**PartitionId**, tal y como se explicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0536-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="c0536-187">También podemos ver que tiene Hola mismo número de particiones como entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="c0536-188">Escenarios de ejemplo que *no* son embarazosamente paralelos</span><span class="sxs-lookup"><span data-stu-id="c0536-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="c0536-189">En la sección anterior de hello, mostramos algunos escenarios embarazosamente paralelas.</span><span class="sxs-lookup"><span data-stu-id="c0536-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="c0536-190">En esta sección, se tratan los escenarios que no cumplen todos los requisitos toobe de hello embarazosamente paralelas.</span><span class="sxs-lookup"><span data-stu-id="c0536-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="c0536-191">Recuento de particiones no coincidente</span><span class="sxs-lookup"><span data-stu-id="c0536-191">Mismatched partition count</span></span>
* <span data-ttu-id="c0536-192">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c0536-193">Salida: Event Hubs con 32 particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="c0536-194">En este caso, no importa qué consulta hello es.</span><span class="sxs-lookup"><span data-stu-id="c0536-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="c0536-195">Si el recuento de particiones de entrada de hello no coincide con recuento de particiones de salida de hello, topología hello no embarazosamente paralela.</span><span class="sxs-lookup"><span data-stu-id="c0536-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="c0536-196">No se usa Event Hubs ni Blob Storage como salida</span><span class="sxs-lookup"><span data-stu-id="c0536-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="c0536-197">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c0536-198">Salida: PowerBI</span><span class="sxs-lookup"><span data-stu-id="c0536-198">Output: PowerBI</span></span>

<span data-ttu-id="c0536-199">La salida de PowerBI no admite en este momento la creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="c0536-200">Por consiguiente, este escenario no es embarazosamente paralelo.</span><span class="sxs-lookup"><span data-stu-id="c0536-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="c0536-201">Consulta de varios pasos con diferentes valores de Partition By</span><span class="sxs-lookup"><span data-stu-id="c0536-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="c0536-202">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c0536-203">Salida: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="c0536-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="c0536-204">Consulta:</span><span class="sxs-lookup"><span data-stu-id="c0536-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="c0536-205">Como puede ver, Hola segundo paso utiliza **TollBoothId** como Hola clave de partición.</span><span class="sxs-lookup"><span data-stu-id="c0536-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="c0536-206">Este paso es Hola mismo no como primer paso de hello y, por lo tanto, requiere nos toodo un orden aleatorio.</span><span class="sxs-lookup"><span data-stu-id="c0536-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="c0536-207">Hello ejemplos anteriores muestran algunos trabajos de análisis de transmisiones que se ajustan demasiado (o no) en una topología embarazosamente paralela.</span><span class="sxs-lookup"><span data-stu-id="c0536-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="c0536-208">Si cumple, tienen el potencial de Hola para maximizar su alcance.</span><span class="sxs-lookup"><span data-stu-id="c0536-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="c0536-209">En el caso de los trabajos que no se ajustan a uno de estos perfiles, habrá una guía de escalado disponible en futuras actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="c0536-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="c0536-210">Por ahora, use instrucciones generales de Hola de hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="c0536-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="c0536-211">Calcular la capacidad máxima de transmisión por secuencias Hola de un trabajo</span><span class="sxs-lookup"><span data-stu-id="c0536-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="c0536-212">número total de Hola de unidades de streaming que puede usarse en un trabajo de análisis de transmisiones depende de número de Hola de pasos en la consulta de hello definido para el trabajo de Hola y el número de Hola de particiones para cada paso.</span><span class="sxs-lookup"><span data-stu-id="c0536-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="c0536-213">Pasos de una consulta</span><span class="sxs-lookup"><span data-stu-id="c0536-213">Steps in a query</span></span>
<span data-ttu-id="c0536-214">Una consulta puede tener uno o varios pasos.</span><span class="sxs-lookup"><span data-stu-id="c0536-214">A query can have one or many steps.</span></span> <span data-ttu-id="c0536-215">Cada paso es una subconsulta definida por hello **WITH** palabra clave.</span><span class="sxs-lookup"><span data-stu-id="c0536-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="c0536-216">consulta de Hola que está fuera de hello **WITH** palabra clave (sólo una consulta) también se considera como un paso, como hello **seleccione** instrucción Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="c0536-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="c0536-217">Esta consulta tiene dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c0536-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="c0536-218">Esta consulta se explica con más detalle más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="c0536-219">Posicionamiento de un paso</span><span class="sxs-lookup"><span data-stu-id="c0536-219">Partition a step</span></span>
<span data-ttu-id="c0536-220">Un paso de creación de particiones requiere Hola condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="c0536-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="c0536-221">origen de entrada de Hello debe estar particionado.</span><span class="sxs-lookup"><span data-stu-id="c0536-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="c0536-222">Hola **seleccione** debe leer la instrucción de consulta de Hola desde un origen de entrada con particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="c0536-223">consulta de Hello en el paso de Hola debe tener hello **Partition By** palabra clave.</span><span class="sxs-lookup"><span data-stu-id="c0536-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="c0536-224">Cuando una consulta tiene particiones, los eventos de entrada de hello son grupos de procesado y se agregan en partición independiente y salidas de eventos se generan para cada uno de los grupos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="c0536-225">Si desea un agregado combinado, debe crear un segundo tooaggregate paso sin particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="c0536-226">Calcular el número máximo de hello unidades para un trabajo de streaming</span><span class="sxs-lookup"><span data-stu-id="c0536-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="c0536-227">Juntos, todos los pasos de particiones no pueden escalar un toosix unidades (SUs) para un trabajo de análisis de transmisiones de streaming.</span><span class="sxs-lookup"><span data-stu-id="c0536-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="c0536-228">deben estar particionados SUs tooadd, un paso.</span><span class="sxs-lookup"><span data-stu-id="c0536-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="c0536-229">Cada partición puede tener seis unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="c0536-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="c0536-230">Consultar</span><span class="sxs-lookup"><span data-stu-id="c0536-230">Query</span></span></th><th><span data-ttu-id="c0536-231">SUs máximo para el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="c0536-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="c0536-232">consulta de Hello contiene un solo paso.</span><span class="sxs-lookup"><span data-stu-id="c0536-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="c0536-233">paso de Hello no tiene particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c0536-234">6</span><span class="sxs-lookup"><span data-stu-id="c0536-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="c0536-235">flujo de datos de entrada de Hola se particiona por 3.</span><span class="sxs-lookup"><span data-stu-id="c0536-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="c0536-236">consulta de Hello contiene un solo paso.</span><span class="sxs-lookup"><span data-stu-id="c0536-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="c0536-237">paso de Hello tiene particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c0536-238">18</span><span class="sxs-lookup"><span data-stu-id="c0536-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="c0536-239">consulta de Hello incluye dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c0536-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="c0536-240">Ninguno de los pasos de hello tiene particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c0536-241">6</span><span class="sxs-lookup"><span data-stu-id="c0536-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="c0536-242">flujo de datos de entrada de Hola se particiona por 3.</span><span class="sxs-lookup"><span data-stu-id="c0536-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="c0536-243">consulta de Hello incluye dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c0536-243">hello query contains two steps.</span></span> <span data-ttu-id="c0536-244">paso de entrada de Hola se divide y no es el segundo paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="c0536-245">Hola <strong>seleccione</strong> instrucción lee de la entrada de hello con particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c0536-246">24 (18 para los pasos particionados y 6 para los pasos no particionados)</span><span class="sxs-lookup"><span data-stu-id="c0536-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="c0536-247">Ejemplos de escalado</span><span class="sxs-lookup"><span data-stu-id="c0536-247">Examples of scaling</span></span>

<span data-ttu-id="c0536-248">Hello siguiente consulta calcula Hola número de automóviles dentro de una ventana de tres minutos que se va a través de una estación de peaje que tiene tres casetas de cuota.</span><span class="sxs-lookup"><span data-stu-id="c0536-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="c0536-249">Esta consulta se puede ampliar SUs toosix.</span><span class="sxs-lookup"><span data-stu-id="c0536-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c0536-250">toouse más SUs para Hola consulta, ambos Hola flujo de datos de entrada y consulta de hello debe estar particionado.</span><span class="sxs-lookup"><span data-stu-id="c0536-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="c0536-251">Como partición de flujo de datos de Hola se establece too3, hello siguiente consulta modificada se puede ampliar SUs too18:</span><span class="sxs-lookup"><span data-stu-id="c0536-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c0536-252">Cuando una consulta tiene particiones, los eventos de entrada de Hola se procesan y se agregan en grupos de partición independiente.</span><span class="sxs-lookup"><span data-stu-id="c0536-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="c0536-253">También se genera el evento de salida para cada uno de los grupos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="c0536-254">Creación de particiones puede provocar algunos resultados inesperados cuando hello **GROUP BY** campo no es de clave de partición de hello en el flujo de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="c0536-255">Por ejemplo, hello **TollBoothId** campo de consulta anterior hello no es clave de partición de Hola de **Entrada1**.</span><span class="sxs-lookup"><span data-stu-id="c0536-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="c0536-256">resultado de Hello es ese hello datos entre cabinas #1 pueden propagarse en varias particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="c0536-257">Cada uno de hello **Entrada1** particiones se procesarán por separado mediante análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="c0536-258">Como resultado, varios registros de recuento de automóvil Hola para Hola mismo cabinas Hola se creará la misma ventana de saltos de tamaño constante.</span><span class="sxs-lookup"><span data-stu-id="c0536-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="c0536-259">Si no se puede cambiar la clave de partición de entrada de hello, puede solucionar este problema mediante la adición de un paso de partición que no es, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c0536-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="c0536-260">Esta consulta puede ser SUs too24 escalado.</span><span class="sxs-lookup"><span data-stu-id="c0536-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="c0536-261">Si va a unir dos flujos, asegúrese de que secuencias Hola se dividen en particiones por clave de partición de Hola de columna de Hola que usar toocreate Hola combinaciones.</span><span class="sxs-lookup"><span data-stu-id="c0536-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="c0536-262">También asegúrese de que dispone de hello mismo número de particiones en ambas secuencias.</span><span class="sxs-lookup"><span data-stu-id="c0536-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="c0536-263">Configuración de las unidades de streaming de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c0536-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="c0536-264">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0536-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c0536-265">En lista de Hola de recursos, busque el trabajo de análisis de transmisiones de Hola que desee tooscale y, a continuación, vuelva a abrirlo.</span><span class="sxs-lookup"><span data-stu-id="c0536-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="c0536-266">Hola trabajo hoja, en **configurar**, haga clic en **escala**.</span><span class="sxs-lookup"><span data-stu-id="c0536-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Configuración del trabajo de Stream Analytics en Azure Portal][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="c0536-268">Use Hola control deslizante tooset Hola SUs trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="c0536-269">Observe que son valores de SU toospecific limitado.</span><span class="sxs-lookup"><span data-stu-id="c0536-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="c0536-270">Supervisión del rendimiento del trabajo</span><span class="sxs-lookup"><span data-stu-id="c0536-270">Monitor job performance</span></span>
<span data-ttu-id="c0536-271">Con hello portal de Azure, puede seguir el rendimiento de un trabajo hello:</span><span class="sxs-lookup"><span data-stu-id="c0536-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Trabajos de supervisión de Análisis de transmisiones de Azure][img.stream.analytics.monitor.job]

<span data-ttu-id="c0536-273">Calcular el rendimiento de hello esperada de carga de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0536-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="c0536-274">Si el rendimiento de hello es inferior a lo esperado, optimizar partición entrada hello, optimizar la consulta de Hola y agregar SUs tooyour trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0536-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="c0536-275">Visualizar el rendimiento de análisis de transmisiones a escala: escenario de frambuesa Pi Hola</span><span class="sxs-lookup"><span data-stu-id="c0536-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="c0536-276">toohelp que comprender cómo escalar trabajos de análisis de transmisiones, se ha realizado un experimento basado en la entrada desde un dispositivo de frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="c0536-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="c0536-277">Este experimento nos permite ver el efecto de hello en el rendimiento de varias particiones y unidades de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="c0536-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="c0536-278">En este escenario, el dispositivo de hello envía concentrador de eventos de tooan de sensor datos (clientes).</span><span class="sxs-lookup"><span data-stu-id="c0536-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="c0536-279">Análisis de transmisión por secuencias procesa los datos de Hola y envía una alerta o estadísticas como un concentrador de eventos de tooanother de salida.</span><span class="sxs-lookup"><span data-stu-id="c0536-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="c0536-280">cliente de Hello envía los datos de sensor en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c0536-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="c0536-281">salida de datos de Hello también está en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c0536-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="c0536-282">datos de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="c0536-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="c0536-283">Hola después de consulta es toosend usa una alerta cuando se desactiva una luz:</span><span class="sxs-lookup"><span data-stu-id="c0536-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="c0536-284">Medición de la capacidad de procesamiento</span><span class="sxs-lookup"><span data-stu-id="c0536-284">Measure throughput</span></span>

<span data-ttu-id="c0536-285">En este contexto, el rendimiento es la cantidad de Hola de datos de entrada procesados por el análisis de transmisiones en una cantidad fija de tiempo.</span><span class="sxs-lookup"><span data-stu-id="c0536-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="c0536-286">(Se mide durante 10 minutos). tooachieve Hola mejor procesamiento de rendimiento para hello los datos de entrada, ambos Hola flujo entrada y consulta Hola se divide en particiones.</span><span class="sxs-lookup"><span data-stu-id="c0536-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="c0536-287">Hemos incluido **COUNT()** en hello consulta toomeasure se han procesado la cantidad de eventos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c0536-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="c0536-288">trabajo de hello seguro toomake no estaba esperando simplemente toocome de eventos de entrada, cada partición del concentrador de eventos de entrada de Hola se haya cargado previamente con unos 300 MB de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c0536-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="c0536-289">Hello tabla siguiente muestra los resultados de hello que vimos cuando aumentamos número Hola de unidades de streaming y recuentos de partición correspondiente hello en los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="c0536-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="c0536-290">Particiones de entrada</span><span class="sxs-lookup"><span data-stu-id="c0536-290">Input Partitions</span></span></th><th><span data-ttu-id="c0536-291">Particiones de salida</span><span class="sxs-lookup"><span data-stu-id="c0536-291">Output Partitions</span></span></th><th><span data-ttu-id="c0536-292">Unidades de streaming</span><span class="sxs-lookup"><span data-stu-id="c0536-292">Streaming Units</span></span></th><th><span data-ttu-id="c0536-293">Capacidad de procesamiento sostenida</span><span class="sxs-lookup"><span data-stu-id="c0536-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="c0536-294">12</span><span class="sxs-lookup"><span data-stu-id="c0536-294">12</span></span></td>
<td><span data-ttu-id="c0536-295">12</span><span class="sxs-lookup"><span data-stu-id="c0536-295">12</span></span></td>
<td><span data-ttu-id="c0536-296">6</span><span class="sxs-lookup"><span data-stu-id="c0536-296">6</span></span></td>
<td><span data-ttu-id="c0536-297">4,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="c0536-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c0536-298">12</span><span class="sxs-lookup"><span data-stu-id="c0536-298">12</span></span></td>
<td><span data-ttu-id="c0536-299">12</span><span class="sxs-lookup"><span data-stu-id="c0536-299">12</span></span></td>
<td><span data-ttu-id="c0536-300">12</span><span class="sxs-lookup"><span data-stu-id="c0536-300">12</span></span></td>
<td><span data-ttu-id="c0536-301">8,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="c0536-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c0536-302">48</span><span class="sxs-lookup"><span data-stu-id="c0536-302">48</span></span></td>
<td><span data-ttu-id="c0536-303">48</span><span class="sxs-lookup"><span data-stu-id="c0536-303">48</span></span></td>
<td><span data-ttu-id="c0536-304">48</span><span class="sxs-lookup"><span data-stu-id="c0536-304">48</span></span></td>
<td><span data-ttu-id="c0536-305">38,32 MB/s</span><span class="sxs-lookup"><span data-stu-id="c0536-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c0536-306">192</span><span class="sxs-lookup"><span data-stu-id="c0536-306">192</span></span></td>
<td><span data-ttu-id="c0536-307">192</span><span class="sxs-lookup"><span data-stu-id="c0536-307">192</span></span></td>
<td><span data-ttu-id="c0536-308">192</span><span class="sxs-lookup"><span data-stu-id="c0536-308">192</span></span></td>
<td><span data-ttu-id="c0536-309">172,67 MB/s</span><span class="sxs-lookup"><span data-stu-id="c0536-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c0536-310">480</span><span class="sxs-lookup"><span data-stu-id="c0536-310">480</span></span></td>
<td><span data-ttu-id="c0536-311">480</span><span class="sxs-lookup"><span data-stu-id="c0536-311">480</span></span></td>
<td><span data-ttu-id="c0536-312">480</span><span class="sxs-lookup"><span data-stu-id="c0536-312">480</span></span></td>
<td><span data-ttu-id="c0536-313">454,27 MB/s</span><span class="sxs-lookup"><span data-stu-id="c0536-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c0536-314">720</span><span class="sxs-lookup"><span data-stu-id="c0536-314">720</span></span></td>
<td><span data-ttu-id="c0536-315">720</span><span class="sxs-lookup"><span data-stu-id="c0536-315">720</span></span></td>
<td><span data-ttu-id="c0536-316">720</span><span class="sxs-lookup"><span data-stu-id="c0536-316">720</span></span></td>
<td><span data-ttu-id="c0536-317">609,69 MB/s</span><span class="sxs-lookup"><span data-stu-id="c0536-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="c0536-318">Y hello gráfico siguiente muestra una visualización de relación de hello entre SUs y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c0536-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![IMG.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="c0536-320">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="c0536-320">Get help</span></span>
<span data-ttu-id="c0536-321">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c0536-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0536-322">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0536-322">Next steps</span></span>
* [<span data-ttu-id="c0536-323">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="c0536-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c0536-324">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c0536-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c0536-325">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="c0536-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c0536-326">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c0536-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

