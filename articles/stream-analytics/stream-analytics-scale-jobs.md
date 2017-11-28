---
title: Escalar los trabajos de Stream Analytics para incrementar el rendimiento | Microsoft Docs
description: "Aprenda a escalar los trabajos de Análisis de transmisiones mediante la configuración de particiones de entrada, la optimización de la definición de consulta y el ajuste de las unidades de streaming del trabajo."
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
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="af680-104">Escalado de trabajos de Análisis de transmisiones de Azure para incrementar el rendimiento de procesamiento de flujo de datos</span><span class="sxs-lookup"><span data-stu-id="af680-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="af680-105">En este artículo se muestra cómo ajustar una consulta de Stream Analytics para aumentar la capacidad de procesamiento de trabajos de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="af680-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="af680-106">Aprenda a escalar los trabajos de Stream Analytics mediante la configuración de particiones de entrada, el ajuste de la definición de consulta y el cálculo y establecimiento de las *unidades de streaming* (SU) del trabajo.</span><span class="sxs-lookup"><span data-stu-id="af680-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="af680-107">¿Cuáles son las partes de un trabajo de Análisis de transmisiones?</span><span class="sxs-lookup"><span data-stu-id="af680-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="af680-108">Una definición de trabajo de Análisis de transmisiones incluye entradas, una consulta y la salida.</span><span class="sxs-lookup"><span data-stu-id="af680-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="af680-109">Las entradas proceden del lugar en el cual el trabajo lee el flujo de datos.</span><span class="sxs-lookup"><span data-stu-id="af680-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="af680-110">La consulta se usa para transformar el flujo de entrada de datos y la salida es el lugar al que el trabajo envía los resultados.</span><span class="sxs-lookup"><span data-stu-id="af680-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="af680-111">Un trabajo requiere al menos un origen de entrada de streaming de datos.</span><span class="sxs-lookup"><span data-stu-id="af680-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="af680-112">El origen de entrada del flujo de datos puede almacenarse en un centro de eventos de Azure o en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="af680-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="af680-113">Para más información, vea [¿Qué es Azure Stream Analytics?](stream-analytics-introduction.md) e [Introducción al uso de Azure Stream Analytics: detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="af680-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="af680-114">Particiones en Event Hubs y Azure Storage</span><span class="sxs-lookup"><span data-stu-id="af680-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="af680-115">El escalado de un trabajo de Stream Analytics aprovecha las particiones en la entrada o la salida.</span><span class="sxs-lookup"><span data-stu-id="af680-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="af680-116">La creación de particiones permite dividir los datos en subconjuntos en función de una clave de partición.</span><span class="sxs-lookup"><span data-stu-id="af680-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="af680-117">Un proceso que consume los datos (por ejemplo, un trabajo de Stream Analytics) puede consumir y escribir diferentes particiones en paralelo, lo que aumenta la capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="af680-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="af680-118">Si trabaja con Stream Analytics, puede aprovechar las ventajas de las particiones en Event Hubs y Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="af680-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="af680-119">Para más información sobre las particiones, vea los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="af680-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="af680-120">Información general de las características de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="af680-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="af680-121">Creación de particiones de datos</span><span class="sxs-lookup"><span data-stu-id="af680-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="af680-122">Unidades de streaming (SU)</span><span class="sxs-lookup"><span data-stu-id="af680-122">Streaming units (SUs)</span></span>
<span data-ttu-id="af680-123">Las unidades de streaming (SU) representan los recursos y la capacidad informática que se necesitan para ejecutar un trabajo de Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="af680-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="af680-124">Las SU proporcionan una forma de describir la capacidad de procesamiento del evento relativo en función de una medida que combina la CPU, la memoria y las tasas de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="af680-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="af680-125">Cada unidad de streaming corresponde aproximadamente a 1 MB por segundo de capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="af680-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="af680-126">La elección del número de unidades de streaming que se necesitan para un trabajo en concreto depende de la configuración de particiones para las entradas y de la consulta definida para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="af680-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="af680-127">Puede seleccionar como máximo su cuota en unidades de streaming para un trabajo.</span><span class="sxs-lookup"><span data-stu-id="af680-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="af680-128">De manera predeterminada, cada suscripción de Azure tiene una cuota máxima de 50 unidades de streaming en todos los trabajos de análisis de una región específica.</span><span class="sxs-lookup"><span data-stu-id="af680-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="af680-129">Para aumentar las unidades de streaming de sus suscripciones, contacte con [Soporte técnico de Microsoft](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="af680-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="af680-130">Los valores válidos para unidades de streaming por trabajo son 1, 3, 6 y más en incrementos de 6.</span><span class="sxs-lookup"><span data-stu-id="af680-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="af680-131">Trabajos embarazosamente paralelos</span><span class="sxs-lookup"><span data-stu-id="af680-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="af680-132">Un trabajo *embarazosamente paralelo* es el escenario más escalable que tenemos en Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="af680-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="af680-133">Conecta una partición de la entrada en una instancia de la consulta a una partición de la salida.</span><span class="sxs-lookup"><span data-stu-id="af680-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="af680-134">Este paralelismo tiene los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="af680-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="af680-135">Si la lógica de la consulta depende de la misma clave que procesa la misma instancia de consulta, ha de asegurarse de que los eventos vayan a la misma partición de la entrada.</span><span class="sxs-lookup"><span data-stu-id="af680-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="af680-136">En Event Hubs, esto significa que los datos del evento deben tener establecido el valor **PartitionKey**.</span><span class="sxs-lookup"><span data-stu-id="af680-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="af680-137">También puede usar remitentes con particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="af680-138">En Blob Storage, esto significa que los eventos se envían a la misma carpeta de partición.</span><span class="sxs-lookup"><span data-stu-id="af680-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="af680-139">Si la lógica de consulta no requiere que la misma instancia de consulta procese la misma clave, puede ignorar este requisito.</span><span class="sxs-lookup"><span data-stu-id="af680-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="af680-140">Un ejemplo de esta lógica sería una sencilla consulta select-project-filter.</span><span class="sxs-lookup"><span data-stu-id="af680-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="af680-141">Una vez dispuestos los datos en la salida, hay que asegurarse de que la consulta está particionada.</span><span class="sxs-lookup"><span data-stu-id="af680-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="af680-142">Esto requiere el uso de **Partition By** en todos los pasos.</span><span class="sxs-lookup"><span data-stu-id="af680-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="af680-143">Se pueden usar varios pasos, pero todos deben particionarse con la misma clave.</span><span class="sxs-lookup"><span data-stu-id="af680-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="af680-144">Actualmente, la clave de partición debe establecerse en **PartitionId** para que el trabajo sea totalmente paralelo.</span><span class="sxs-lookup"><span data-stu-id="af680-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="af680-145">Solo Event Hubs y Blob Storage admiten en este momento salidas con particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="af680-146">En la salida de Event Hubs, debe configurar la clave de partición para que sea **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="af680-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="af680-147">En la salida de Blob Storage, no tiene que hacer nada.</span><span class="sxs-lookup"><span data-stu-id="af680-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="af680-148">El número de particiones de entrada debe ser igual al número de particiones de salida.</span><span class="sxs-lookup"><span data-stu-id="af680-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="af680-149">La salida de Blob Storage no admite en este momento la creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="af680-150">Pero no importa, porque hereda el esquema de partición de la consulta ascendente.</span><span class="sxs-lookup"><span data-stu-id="af680-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="af680-151">Vea ejemplos de valores de partición que permiten un trabajo totalmente paralelo:</span><span class="sxs-lookup"><span data-stu-id="af680-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="af680-152">Ocho particiones de entrada de Event Hubs y ocho particiones de salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="af680-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="af680-153">Ocho particiones de entrada de Event Hubs y salida de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="af680-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="af680-154">Ocho particiones de entrada de Blob Storage y salida de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="af680-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="af680-155">Ocho particiones de entrada de Blob Storage y ocho particiones de salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="af680-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="af680-156">En las siguientes secciones se describen algunos escenarios de ejemplo que son embarazosamente paralelos.</span><span class="sxs-lookup"><span data-stu-id="af680-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="af680-157">Consulta sencilla</span><span class="sxs-lookup"><span data-stu-id="af680-157">Simple query</span></span>

* <span data-ttu-id="af680-158">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="af680-159">Salida: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="af680-160">Consulta:</span><span class="sxs-lookup"><span data-stu-id="af680-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="af680-161">Esta consulta es un filtro sencillo.</span><span class="sxs-lookup"><span data-stu-id="af680-161">This query is a simple filter.</span></span> <span data-ttu-id="af680-162">Por consiguiente, no hay que preocuparse por crear particiones en la entrada que se envía al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="af680-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="af680-163">Observe que la consulta incluye **Partition By PartitionId**, por lo que cumple el requisito 2 de antes.</span><span class="sxs-lookup"><span data-stu-id="af680-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="af680-164">En cuanto a la salida, es preciso configurar la salida del centro de eventos en el trabajo para que el la clave de partición se establezca en **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="af680-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="af680-165">Una última comprobación consiste en asegurarse de que el número de particiones de entrada es igual al número de particiones de salida.</span><span class="sxs-lookup"><span data-stu-id="af680-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="af680-166">Consulta con una clave de agrupación</span><span class="sxs-lookup"><span data-stu-id="af680-166">Query with a grouping key</span></span>

* <span data-ttu-id="af680-167">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="af680-168">Salida: Blob Storage</span><span class="sxs-lookup"><span data-stu-id="af680-168">Output: Blob storage</span></span>

<span data-ttu-id="af680-169">Consulta:</span><span class="sxs-lookup"><span data-stu-id="af680-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="af680-170">Esta consulta tiene una clave de agrupación.</span><span class="sxs-lookup"><span data-stu-id="af680-170">This query has a grouping key.</span></span> <span data-ttu-id="af680-171">Por lo tanto, es preciso que la misma clave se procese en la misma instancia de consulta, lo que significa que deben enviarse eventos al centro de eventos de manera particionada.</span><span class="sxs-lookup"><span data-stu-id="af680-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="af680-172">¿Pero qué clave debe usarse?</span><span class="sxs-lookup"><span data-stu-id="af680-172">But which key should be used?</span></span> <span data-ttu-id="af680-173">**PartitionId** es un concepto de lógica de trabajos.</span><span class="sxs-lookup"><span data-stu-id="af680-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="af680-174">La clave que realmente importa es **TollBoothId**, por lo que el valor **PartitionKey** de los datos de evento debe ser **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="af680-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="af680-175">Esto se hace en esta consulta estableciendo **Partition By** en **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="af680-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="af680-176">Puesto que la salida es Blob Storage, no hay que preocuparse en configurar un valor de clave de partición, como estipula el requisito 4.</span><span class="sxs-lookup"><span data-stu-id="af680-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="af680-177">Consulta de varios pasos con una clave de agrupación</span><span class="sxs-lookup"><span data-stu-id="af680-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="af680-178">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="af680-179">Salida: instancia de Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="af680-180">Consulta:</span><span class="sxs-lookup"><span data-stu-id="af680-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="af680-181">Esta consulta tiene una clave de agrupación, por lo que es necesario que la misma instancia de procese la misma clave.</span><span class="sxs-lookup"><span data-stu-id="af680-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="af680-182">Se puede usar la misma estrategia que en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="af680-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="af680-183">En este caso, la consulta tiene varios pasos.</span><span class="sxs-lookup"><span data-stu-id="af680-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="af680-184">¿Cada paso tiene **Partition By PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="af680-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="af680-185">Sí, por lo que la consulta cumple el requisito 3.</span><span class="sxs-lookup"><span data-stu-id="af680-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="af680-186">En cuanto a la salida, es necesario establecer la clave de partición en **PartitionId**, tal y como se ha explicado antes.</span><span class="sxs-lookup"><span data-stu-id="af680-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="af680-187">También puede verse que tiene el mismo número de particiones que la entrada.</span><span class="sxs-lookup"><span data-stu-id="af680-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="af680-188">Escenarios de ejemplo que *no* son embarazosamente paralelos</span><span class="sxs-lookup"><span data-stu-id="af680-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="af680-189">En la sección anterior, se han mostrado algunos escenarios embarazosamente paralelos.</span><span class="sxs-lookup"><span data-stu-id="af680-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="af680-190">En esta sección se describen escenarios en los que no se cumplen todos los requisitos para que sean embarazosamente paralelos.</span><span class="sxs-lookup"><span data-stu-id="af680-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="af680-191">Recuento de particiones no coincidente</span><span class="sxs-lookup"><span data-stu-id="af680-191">Mismatched partition count</span></span>
* <span data-ttu-id="af680-192">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="af680-193">Salida: Event Hubs con 32 particiones</span><span class="sxs-lookup"><span data-stu-id="af680-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="af680-194">En este caso, no importa cuál es la consulta.</span><span class="sxs-lookup"><span data-stu-id="af680-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="af680-195">Si el recuento de particiones de entrada no coincide con el recuento de particiones de salida, la topología no es embarazosamente paralela.</span><span class="sxs-lookup"><span data-stu-id="af680-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="af680-196">No se usa Event Hubs ni Blob Storage como salida</span><span class="sxs-lookup"><span data-stu-id="af680-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="af680-197">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="af680-198">Salida: PowerBI</span><span class="sxs-lookup"><span data-stu-id="af680-198">Output: PowerBI</span></span>

<span data-ttu-id="af680-199">La salida de PowerBI no admite en este momento la creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="af680-200">Por consiguiente, este escenario no es embarazosamente paralelo.</span><span class="sxs-lookup"><span data-stu-id="af680-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="af680-201">Consulta de varios pasos con diferentes valores de Partition By</span><span class="sxs-lookup"><span data-stu-id="af680-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="af680-202">Entrada: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="af680-203">Salida: Event Hubs con ocho particiones</span><span class="sxs-lookup"><span data-stu-id="af680-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="af680-204">Consulta:</span><span class="sxs-lookup"><span data-stu-id="af680-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="af680-205">Como puede ver, el segundo paso utiliza **TollBoothId** como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="af680-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="af680-206">Este paso no es igual al primer paso y, por tanto, hay que seguir un orden aleatorio.</span><span class="sxs-lookup"><span data-stu-id="af680-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="af680-207">Los ejemplos anteriores muestran algunos trabajos de Stream Analytics que se ajustan (o no) a una topología embarazosamente paralela.</span><span class="sxs-lookup"><span data-stu-id="af680-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="af680-208">Si se ajustan, tienen posibilidades de alcanzar la escala máxima.</span><span class="sxs-lookup"><span data-stu-id="af680-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="af680-209">En el caso de los trabajos que no se ajustan a uno de estos perfiles, habrá una guía de escalado disponible en futuras actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="af680-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="af680-210">Por ahora, use la guía general en las siguientes secciones.</span><span class="sxs-lookup"><span data-stu-id="af680-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="af680-211">Cálculo de las unidades máximas de streaming para un trabajo</span><span class="sxs-lookup"><span data-stu-id="af680-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="af680-212">El número total de unidades de streaming que se puede utilizar en un trabajo de Stream Analytics depende del número de pasos de la consulta definida para el trabajo y del número de particiones para cada paso.</span><span class="sxs-lookup"><span data-stu-id="af680-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="af680-213">Pasos de una consulta</span><span class="sxs-lookup"><span data-stu-id="af680-213">Steps in a query</span></span>
<span data-ttu-id="af680-214">Una consulta puede tener uno o varios pasos.</span><span class="sxs-lookup"><span data-stu-id="af680-214">A query can have one or many steps.</span></span> <span data-ttu-id="af680-215">Cada paso es una subconsulta definida mediante la palabra clave **WITH**.</span><span class="sxs-lookup"><span data-stu-id="af680-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="af680-216">La consulta que queda al margen de la palabra clave **WITH** (una sola consulta) también se cuenta como un paso; por ejemplo, la instrucción **SELECT** de la consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="af680-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="af680-217">Esta consulta tiene dos pasos.</span><span class="sxs-lookup"><span data-stu-id="af680-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="af680-218">Esta consulta se analiza con más detalle más adelante en el artículo.</span><span class="sxs-lookup"><span data-stu-id="af680-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="af680-219">Posicionamiento de un paso</span><span class="sxs-lookup"><span data-stu-id="af680-219">Partition a step</span></span>
<span data-ttu-id="af680-220">El particionamiento de un paso requiere las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="af680-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="af680-221">El origen de entrada debe tener particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="af680-222">La instrucción **SELECT** de la consulta debe leer desde un origen de entrada particionada.</span><span class="sxs-lookup"><span data-stu-id="af680-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="af680-223">La consulta comprendida en el paso debe incluir la palabra clave **Partition By**.</span><span class="sxs-lookup"><span data-stu-id="af680-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="af680-224">Cuando una consulta está particionada, los eventos de entrada se procesan y agregan en grupos de particiones independientes, y se generan eventos de salida para cada uno de los grupos.</span><span class="sxs-lookup"><span data-stu-id="af680-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="af680-225">Si quiere usar un agregado combinado, debe crear un segundo paso sin particionar que agregar.</span><span class="sxs-lookup"><span data-stu-id="af680-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="af680-226">Cálculo de las unidades máximas de streaming para un trabajo</span><span class="sxs-lookup"><span data-stu-id="af680-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="af680-227">Todos los pasos sin particiones juntos pueden escalarse hasta seis unidades de streaming (SU) para un trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="af680-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="af680-228">Para agregar unidades de streaming, un paso debe estar particionado.</span><span class="sxs-lookup"><span data-stu-id="af680-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="af680-229">Cada partición puede tener seis unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="af680-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="af680-230">Consultar</span><span class="sxs-lookup"><span data-stu-id="af680-230">Query</span></span></th><th><span data-ttu-id="af680-231">Número máximo de unidades de streaming del trabajo</span><span class="sxs-lookup"><span data-stu-id="af680-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="af680-232">La consulta contiene un solo paso.</span><span class="sxs-lookup"><span data-stu-id="af680-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="af680-233">El paso no está particionado.</span><span class="sxs-lookup"><span data-stu-id="af680-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="af680-234">6</span><span class="sxs-lookup"><span data-stu-id="af680-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="af680-235">La secuencia de datos de entrada está particionada en tres.</span><span class="sxs-lookup"><span data-stu-id="af680-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="af680-236">La consulta contiene un solo paso.</span><span class="sxs-lookup"><span data-stu-id="af680-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="af680-237">El paso está particionado.</span><span class="sxs-lookup"><span data-stu-id="af680-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="af680-238">18</span><span class="sxs-lookup"><span data-stu-id="af680-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="af680-239">La consulta contiene dos pasos.</span><span class="sxs-lookup"><span data-stu-id="af680-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="af680-240">Ninguno de los pasos está particionado.</span><span class="sxs-lookup"><span data-stu-id="af680-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="af680-241">6</span><span class="sxs-lookup"><span data-stu-id="af680-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="af680-242">La secuencia de datos de entrada está particionada en tres.</span><span class="sxs-lookup"><span data-stu-id="af680-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="af680-243">La consulta contiene dos pasos.</span><span class="sxs-lookup"><span data-stu-id="af680-243">The query contains two steps.</span></span> <span data-ttu-id="af680-244">El paso de entrada tiene particiones y el segundo paso no.</span><span class="sxs-lookup"><span data-stu-id="af680-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="af680-245">La instrucción <strong>SELECT</strong> se lee de la entrada particionada.</span><span class="sxs-lookup"><span data-stu-id="af680-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="af680-246">24 (18 para los pasos particionados y 6 para los pasos no particionados)</span><span class="sxs-lookup"><span data-stu-id="af680-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="af680-247">Ejemplos de escalado</span><span class="sxs-lookup"><span data-stu-id="af680-247">Examples of scaling</span></span>

<span data-ttu-id="af680-248">La siguiente consulta calcula el número de vehículos que pasan por una estación de peaje con tres cabinas de peaje en una ventana temporal de tres minutos.</span><span class="sxs-lookup"><span data-stu-id="af680-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="af680-249">Esta consulta se puede escalar hasta seis unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="af680-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="af680-250">Para usar más unidades de streaming en la consulta, el flujo de datos de entrada y la consulta deben estar particionados.</span><span class="sxs-lookup"><span data-stu-id="af680-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="af680-251">Dado que la partición del flujo de datos está establecida en 3, la siguiente consulta modificada puede escalarse hasta 18 unidades de streaming:</span><span class="sxs-lookup"><span data-stu-id="af680-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="af680-252">Cuando una consulta está particionada, se procesan los eventos de entrada y se agregan en grupos de particiones independientes.</span><span class="sxs-lookup"><span data-stu-id="af680-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="af680-253">También se generan eventos de salida para cada uno de los grupos.</span><span class="sxs-lookup"><span data-stu-id="af680-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="af680-254">La creación de particiones puede ocasionar algunos resultados inesperados cuando el campo **GROUP BY** no es la clave de partición del flujo de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="af680-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="af680-255">Por ejemplo, el campo **TollBoothId** de la consulta anterior no es la clave de partición de **Input1**.</span><span class="sxs-lookup"><span data-stu-id="af680-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="af680-256">El resultado es que los datos de la cabina de peaje 1 se pueden distribuir en varias particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="af680-257">Cada una de las particiones de **Input1** se procesará por separado en Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="af680-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="af680-258">Por consiguiente, se crearán varios registros de recuento de vehículos para la misma cabina en la misma ventana de saltos de tamaño constante.</span><span class="sxs-lookup"><span data-stu-id="af680-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="af680-259">Si la clave de partición de entrada no se puede cambiar, este problema se puede solucionar agregando un paso adicional sin particiones, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="af680-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="af680-260">Esta consulta se puede escalar hasta 24 unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="af680-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="af680-261">Si va a combinar dos flujos de datos, asegúrese de que estén particionados mediante la clave de partición de la columna que usa para realizar las combinaciones.</span><span class="sxs-lookup"><span data-stu-id="af680-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="af680-262">Asegúrese también de que tiene el mismo número de particiones en ambos flujos de datos.</span><span class="sxs-lookup"><span data-stu-id="af680-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="af680-263">Configuración de las unidades de streaming de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af680-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="af680-264">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af680-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="af680-265">En la lista de recursos, busque el trabajo de Stream Analytics que quiere escalar y ábralo.</span><span class="sxs-lookup"><span data-stu-id="af680-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="af680-266">En la hoja del trabajo, en **Configurar**, haga clic en **Escala**.</span><span class="sxs-lookup"><span data-stu-id="af680-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Configuración del trabajo de Stream Analytics en Azure Portal][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="af680-268">Use el control deslizante para establecer las unidades de streaming del trabajo.</span><span class="sxs-lookup"><span data-stu-id="af680-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="af680-269">Tenga en cuenta que está limitado a la configuración de unidades de streaming específica.</span><span class="sxs-lookup"><span data-stu-id="af680-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="af680-270">Supervisión del rendimiento del trabajo</span><span class="sxs-lookup"><span data-stu-id="af680-270">Monitor job performance</span></span>
<span data-ttu-id="af680-271">Mediante Azure Portal, puede realizar el seguimiento de la capacidad de procesamiento de un trabajo:</span><span class="sxs-lookup"><span data-stu-id="af680-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Trabajos de supervisión de Análisis de transmisiones de Azure][img.stream.analytics.monitor.job]

<span data-ttu-id="af680-273">Calcule la capacidad de procesamiento esperada de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="af680-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="af680-274">Si la capacidad de procesamiento es inferior a la esperada, ajuste la partición de entrada, ajuste la consulta y agregue unidades de streaming al trabajo.</span><span class="sxs-lookup"><span data-stu-id="af680-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="af680-275">Visualización de la capacidad de procesamiento de Stream Analytics a escala: escenario de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="af680-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="af680-276">Para ayudarle a comprender cómo se escalan los trabajos de Stream Analytics, se ha realizado un experimento basado en un dispositivo Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="af680-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="af680-277">Este experimento permite ver los efectos sobre la capacidad de procesamiento de varias unidades de streaming y particiones.</span><span class="sxs-lookup"><span data-stu-id="af680-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="af680-278">En este escenario, el dispositivo envía datos de sensores (clientes) a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="af680-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="af680-279">Stream Analytics procesa los datos y envía una alerta o estadísticas como salida a otro centro de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="af680-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="af680-280">El cliente envía los datos del sensor en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="af680-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="af680-281">La salida de datos también está en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="af680-281">The data output is also in JSON format.</span></span> <span data-ttu-id="af680-282">Los datos tienen este aspecto:</span><span class="sxs-lookup"><span data-stu-id="af680-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="af680-283">La siguiente consulta se utiliza para enviar una alerta cuando se apaga una luz:</span><span class="sxs-lookup"><span data-stu-id="af680-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="af680-284">Medición de la capacidad de procesamiento</span><span class="sxs-lookup"><span data-stu-id="af680-284">Measure throughput</span></span>

<span data-ttu-id="af680-285">En este contexto, la capacidad de procesamiento es la cantidad de datos de entrada que procesa Stream Analytics en una cantidad fija de tiempo.</span><span class="sxs-lookup"><span data-stu-id="af680-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="af680-286">(Se mide durante 10 minutos). Para conseguir la mejor capacidad de procesamiento de los datos de entrada, tanto la entrada de flujo de datos como la consulta se han particionado.</span><span class="sxs-lookup"><span data-stu-id="af680-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="af680-287">También se incluye **COUNT()** en la consulta para medir el número de eventos de entrada procesados.</span><span class="sxs-lookup"><span data-stu-id="af680-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="af680-288">Para asegurarse de que el trabajo no está esperando simplemente a que lleguen los eventos de entrada, cada partición del centro de eventos de entrada se ha cargado previamente con aproximadamente 300 MB.</span><span class="sxs-lookup"><span data-stu-id="af680-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="af680-289">La siguiente tabla muestra los resultados se observan al aumentar el número de unidades de streaming y los correspondientes recuentos de particiones en Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="af680-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="af680-290">Particiones de entrada</span><span class="sxs-lookup"><span data-stu-id="af680-290">Input Partitions</span></span></th><th><span data-ttu-id="af680-291">Particiones de salida</span><span class="sxs-lookup"><span data-stu-id="af680-291">Output Partitions</span></span></th><th><span data-ttu-id="af680-292">Unidades de streaming</span><span class="sxs-lookup"><span data-stu-id="af680-292">Streaming Units</span></span></th><th><span data-ttu-id="af680-293">Capacidad de procesamiento sostenida</span><span class="sxs-lookup"><span data-stu-id="af680-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="af680-294">12</span><span class="sxs-lookup"><span data-stu-id="af680-294">12</span></span></td>
<td><span data-ttu-id="af680-295">12</span><span class="sxs-lookup"><span data-stu-id="af680-295">12</span></span></td>
<td><span data-ttu-id="af680-296">6</span><span class="sxs-lookup"><span data-stu-id="af680-296">6</span></span></td>
<td><span data-ttu-id="af680-297">4,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="af680-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="af680-298">12</span><span class="sxs-lookup"><span data-stu-id="af680-298">12</span></span></td>
<td><span data-ttu-id="af680-299">12</span><span class="sxs-lookup"><span data-stu-id="af680-299">12</span></span></td>
<td><span data-ttu-id="af680-300">12</span><span class="sxs-lookup"><span data-stu-id="af680-300">12</span></span></td>
<td><span data-ttu-id="af680-301">8,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="af680-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="af680-302">48</span><span class="sxs-lookup"><span data-stu-id="af680-302">48</span></span></td>
<td><span data-ttu-id="af680-303">48</span><span class="sxs-lookup"><span data-stu-id="af680-303">48</span></span></td>
<td><span data-ttu-id="af680-304">48</span><span class="sxs-lookup"><span data-stu-id="af680-304">48</span></span></td>
<td><span data-ttu-id="af680-305">38,32 MB/s</span><span class="sxs-lookup"><span data-stu-id="af680-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="af680-306">192</span><span class="sxs-lookup"><span data-stu-id="af680-306">192</span></span></td>
<td><span data-ttu-id="af680-307">192</span><span class="sxs-lookup"><span data-stu-id="af680-307">192</span></span></td>
<td><span data-ttu-id="af680-308">192</span><span class="sxs-lookup"><span data-stu-id="af680-308">192</span></span></td>
<td><span data-ttu-id="af680-309">172,67 MB/s</span><span class="sxs-lookup"><span data-stu-id="af680-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="af680-310">480</span><span class="sxs-lookup"><span data-stu-id="af680-310">480</span></span></td>
<td><span data-ttu-id="af680-311">480</span><span class="sxs-lookup"><span data-stu-id="af680-311">480</span></span></td>
<td><span data-ttu-id="af680-312">480</span><span class="sxs-lookup"><span data-stu-id="af680-312">480</span></span></td>
<td><span data-ttu-id="af680-313">454,27 MB/s</span><span class="sxs-lookup"><span data-stu-id="af680-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="af680-314">720</span><span class="sxs-lookup"><span data-stu-id="af680-314">720</span></span></td>
<td><span data-ttu-id="af680-315">720</span><span class="sxs-lookup"><span data-stu-id="af680-315">720</span></span></td>
<td><span data-ttu-id="af680-316">720</span><span class="sxs-lookup"><span data-stu-id="af680-316">720</span></span></td>
<td><span data-ttu-id="af680-317">609,69 MB/s</span><span class="sxs-lookup"><span data-stu-id="af680-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="af680-318">Y en el gráfico siguiente se muestra una visualización de la relación entre unidades de streaming y capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="af680-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![IMG.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="af680-320">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="af680-320">Get help</span></span>
<span data-ttu-id="af680-321">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="af680-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af680-322">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af680-322">Next steps</span></span>
* [<span data-ttu-id="af680-323">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af680-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="af680-324">Introducción al uso de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="af680-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="af680-325">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="af680-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="af680-326">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="af680-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

