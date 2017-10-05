---
title: "Incorporación de entradas de datos a trabajos de Stream Analytics | Microsoft Docs"
description: "Obtenga información acerca de cómo enlazar un origen de datos al trabajo de Análisis de transmisiones como entrada de datos de streaming desde los Centros de eventos, o bien como datos de referencia desde el Almacenamiento de blobs."
keywords: entrada de datos, datos de streaming
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="34097-104">Adición de entradas de datos de streaming o datos de referencia a trabajos de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="34097-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="34097-105">Aprenda a enlazar un origen de datos al trabajo de Análisis de transmisiones como entrada de datos de streaming desde los Centros de eventos, o bien como datos de referencia desde el Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="34097-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="34097-106">Los trabajos de Análisis de transmisiones de Azure pueden estar conectados a una entrada de datos, donde cada una define una conexión a un origen de datos existente.</span><span class="sxs-lookup"><span data-stu-id="34097-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="34097-107">A medida que los datos se envían a ese origen de datos, el trabajo de Análisis de transmisiones los consume y los procesa en tiempo real como datos de streaming.</span><span class="sxs-lookup"><span data-stu-id="34097-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="34097-108">Stream Analytics cuenta con integración de primera clase con [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) y [Azure Blob Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) desde dentro y fuera de la suscripción del trabajo.</span><span class="sxs-lookup"><span data-stu-id="34097-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="34097-109">Este artículo es un paso de la [ruta de aprendizaje de Análisis de transmisiones](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="34097-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="34097-110">Entrada de datos: datos de streaming y datos de referencia</span><span class="sxs-lookup"><span data-stu-id="34097-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="34097-111">Hay dos tipos distintos de entradas en Análisis de transmisiones: flujos de datos y datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="34097-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="34097-112">**Secuencias de datos**: los trabajos de Análisis de transmisiones deben incluir, al menos, una entrada de secuencia de datos para que el trabajo la consuma y transforme.</span><span class="sxs-lookup"><span data-stu-id="34097-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="34097-113">Almacenamiento de blobs de Azure y Centros de eventos de Azure se admiten como orígenes de entrada de flujos de datos.</span><span class="sxs-lookup"><span data-stu-id="34097-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="34097-114">Los Centros de eventos de Azure se usan para recopilar transmisiones de eventos desde dispositivos conectados, servicios y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="34097-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="34097-115">El almacenamiento de blobs de Azure puede usarse como origen de entrada para la ingesta de datos en masa como secuencia.</span><span class="sxs-lookup"><span data-stu-id="34097-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="34097-116">**Datos de referencia**: Análisis de transmisiones admite un segundo tipo de entrada auxiliar denominada datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="34097-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="34097-117">A diferencia de los datos en movimiento, estos datos son estáticos o están desacelerando los cambios.</span><span class="sxs-lookup"><span data-stu-id="34097-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="34097-118">Normalmente se usa para realizar búsquedas y correlaciones con secuencias de datos para crear un conjunto de datos más amplio.</span><span class="sxs-lookup"><span data-stu-id="34097-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="34097-119">Almacenamiento de blobs de Azure es el único origen de entrada admitido actualmente para los datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="34097-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="34097-120">Para agregar una entrada a su trabajo de Análisis de transmisiones:</span><span class="sxs-lookup"><span data-stu-id="34097-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="34097-121">En Azure Portal, haga clic en **Entradas** y en **Agregar una entrada** en el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="34097-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portal de Azure clásico: agregar entrada.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="34097-123">En el Portal de Azure, haga clic en el icono **Entradas** en el trabajo de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="34097-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portal de Azure: agregar entrada.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="34097-125">Especifique el tipo de la entrada: **Flujo de datos** o **Datos de referencia**.</span><span class="sxs-lookup"><span data-stu-id="34097-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Adición de la entrada correcta de datos, de streaming o de referencia](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Adición de la entrada correcta de datos, de streaming o de referencia](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="34097-128">Si crea una entrada de Flujo de datos, especifique el tipo de origen para la entrada.</span><span class="sxs-lookup"><span data-stu-id="34097-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="34097-129">Este paso se omite durante la creación de Datos de referencia ya que, en este momento, solo se admite el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="34097-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Adición de entrada de datos de flujo de datos](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Adición de entrada de datos de flujo de datos](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="34097-132">Asigne un nombre descriptivo para esta entrada en el cuadro Alias de entrada.</span><span class="sxs-lookup"><span data-stu-id="34097-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="34097-133">Este nombre se usará en la consulta de su trabajo más adelante para hacer referencia a la entrada.</span><span class="sxs-lookup"><span data-stu-id="34097-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="34097-134">Rellene el resto de las propiedades de conexión necesarias para conectarse a su origen de datos.</span><span class="sxs-lookup"><span data-stu-id="34097-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="34097-135">Estos campos varían según el tipo de entrada y de origen y se definen en detalle [aquí](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="34097-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Adición de entrada de datos de Centro de eventos](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="34097-137">Especifique la configuración de serialización para los datos de entrada:</span><span class="sxs-lookup"><span data-stu-id="34097-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="34097-138">Para asegurarse de que las consultas funcionan según lo previsto, especifique el **Formato de serialización de eventos** de los datos entrantes.</span><span class="sxs-lookup"><span data-stu-id="34097-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="34097-139">Los formatos de serialización compatibles son JSON, CSV y Avro.</span><span class="sxs-lookup"><span data-stu-id="34097-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="34097-140">Compruebe el valor de **Codificación** para los datos.</span><span class="sxs-lookup"><span data-stu-id="34097-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="34097-141">Por el momento, UTF-8 es el único formato de codificación compatible.</span><span class="sxs-lookup"><span data-stu-id="34097-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Configuración de la serialización de datos para la entrada de datos](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Configuración de la serialización de datos para la entrada de datos](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="34097-144">Después de completar la creación de la entrada, el Análisis de transmisiones comprobará que se puede conectar al origen de la entrada.</span><span class="sxs-lookup"><span data-stu-id="34097-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="34097-145">Puede ver el estado de la operación de prueba de conexión en el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="34097-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Prueba de la conexión de la entrada de datos de streaming](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Prueba de la conexión de la entrada de datos de streaming](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="34097-148">Obtener ayuda con las entradas de datos de streaming</span><span class="sxs-lookup"><span data-stu-id="34097-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="34097-149">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="34097-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="34097-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34097-150">Next steps</span></span>
* [<span data-ttu-id="34097-151">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="34097-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="34097-152">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="34097-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="34097-153">Escalación de trabajos de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="34097-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="34097-154">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="34097-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="34097-155">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="34097-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

