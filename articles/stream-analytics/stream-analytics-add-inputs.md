---
title: "trabajos de análisis de transmisiones de tooyour de entrada de datos aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohook seguridad un tooyour de origen de datos análisis de transmisiones de transmisión por secuencias como entrada de datos de los centros de eventos o datos de referencia desde el almacenamiento de blobs de trabajo."
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
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="14de3-104">Agregar una transmisión por secuencias datos de entrada o referencia datos tooa trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14de3-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="14de3-105">Obtenga información acerca de cómo toohook seguridad un tooyour de origen de datos análisis de transmisiones de transmisión por secuencias como entrada de datos de los centros de eventos o datos de referencia desde el almacenamiento de blobs de trabajo.</span><span class="sxs-lookup"><span data-stu-id="14de3-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="14de3-106">Trabajos de análisis de transmisiones de Azure pueden ser de entrada de datos de tooone conectados o más, cada uno de los cuales define un origen de datos existente de conexión tooan.</span><span class="sxs-lookup"><span data-stu-id="14de3-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="14de3-107">Como origen de datos de toothat enviar datos, es utilizado por el trabajo de análisis de transmisiones de Hola y procesan en tiempo real como la transmisión de datos.</span><span class="sxs-lookup"><span data-stu-id="14de3-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="14de3-108">Análisis de transmisiones tiene la integración de primera clase con [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) y [almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tanto dentro como fuera de suscripción del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14de3-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="14de3-109">En este artículo es un paso en hello [ruta de acceso de aprendizaje de análisis de transmisiones](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="14de3-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="14de3-110">Entrada de datos: datos de streaming y datos de referencia</span><span class="sxs-lookup"><span data-stu-id="14de3-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="14de3-111">Hay dos tipos distintos de entradas en Análisis de transmisiones: flujos de datos y datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="14de3-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="14de3-112">**Flujos de datos**: trabajos de análisis de transmisiones deben incluir al menos un datos flujo entrada toobe consumirá y transformará trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="14de3-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="14de3-113">Almacenamiento de blobs de Azure y Centros de eventos de Azure se admiten como orígenes de entrada de flujos de datos.</span><span class="sxs-lookup"><span data-stu-id="14de3-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="14de3-114">Centros de eventos de Azure son secuencias de eventos de toocollect usado desde dispositivos conectados, servicios y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="14de3-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="14de3-115">El almacenamiento de blobs de Azure puede usarse como origen de entrada para la ingesta de datos en masa como secuencia.</span><span class="sxs-lookup"><span data-stu-id="14de3-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="14de3-116">**Datos de referencia**: Análisis de transmisiones admite un segundo tipo de entrada auxiliar denominada datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="14de3-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="14de3-117">Como toodata opuesto en movimiento, estos datos son estáticos o lenta cambiar.</span><span class="sxs-lookup"><span data-stu-id="14de3-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="14de3-118">Se utiliza normalmente para realizar búsquedas y correlaciones con toocreate de flujos de datos un conjunto más completo de datos.</span><span class="sxs-lookup"><span data-stu-id="14de3-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="14de3-119">Almacenamiento de blobs de Azure está actualmente Hola solo admitido el origen de entrada de datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="14de3-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="14de3-120">un trabajo de análisis de transmisiones de entrada tooyour tooadd:</span><span class="sxs-lookup"><span data-stu-id="14de3-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="14de3-121">Hola portal de Azure, haga clic en **entradas** y, a continuación, haga clic en **agregar una entrada** en el trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="14de3-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portal de Azure clásico: agregar entrada.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="14de3-123">Hola portal de Azure, haga clic en hello **entradas** disponer en mosaico en el trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="14de3-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portal de Azure: agregar entrada.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="14de3-125">Especificar tipo de Hola de entrada de hello: cualquier **flujo de datos** o **hacen referencia a datos**.</span><span class="sxs-lookup"><span data-stu-id="14de3-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Agregar datos correctos de Hola de entrada, modos de transmisión o hacer referencia a](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Agregar datos correctos de Hola de entrada, modos de transmisión o hacer referencia a](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="14de3-128">Si crea una entrada de flujo de datos, especifique el tipo de origen de hello para la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="14de3-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="14de3-129">Este paso se omite durante la creación de Datos de referencia ya que, en este momento, solo se admite el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="14de3-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Adición de entrada de datos de flujo de datos](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Adición de entrada de datos de flujo de datos](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="14de3-132">Proporcione un nombre descriptivo para esta entrada en hello cuadro Alias de entrada.</span><span class="sxs-lookup"><span data-stu-id="14de3-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="14de3-133">Este nombre se usará en la consulta de la tarea más adelante en la entrada de toohello de toorefer.</span><span class="sxs-lookup"><span data-stu-id="14de3-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="14de3-134">Rellene el resto de Hola Hola conexión necesaria propiedades tooconnect tooyour del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="14de3-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="14de3-135">Estos campos varían según el tipo de entrada y de origen y se definen en detalle [aquí](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="14de3-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Adición de entrada de datos de Centro de eventos](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="14de3-137">Especifique la configuración de serialización de Hola para datos de entrada de hello:</span><span class="sxs-lookup"><span data-stu-id="14de3-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="14de3-138">toomake seguro de las consultas funcionan de forma Hola que espera, especifique hello **formato de serialización del evento** de los datos entrantes.</span><span class="sxs-lookup"><span data-stu-id="14de3-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="14de3-139">Los formatos de serialización compatibles son JSON, CSV y Avro.</span><span class="sxs-lookup"><span data-stu-id="14de3-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="14de3-140">Comprobar hello **codificación** para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="14de3-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="14de3-141">UTF-8 es Hola solo admite el formato de codificación en este momento.</span><span class="sxs-lookup"><span data-stu-id="14de3-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Configuración de serialización de datos de entrada de datos de Hola](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Configuración de serialización de datos de entrada de datos de Hola](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="14de3-144">Después de completar la creación de entrada de hello, análisis de transmisiones comprobará que se puede conectar el origen de entrada de toohello.</span><span class="sxs-lookup"><span data-stu-id="14de3-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="14de3-145">Puede ver el estado de Hola de hello operación de conexión de prueba en el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="14de3-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Probar conexión de hello transmisión de datos de entrada](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Probar conexión de hello transmisión de datos de entrada](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="14de3-148">Obtener ayuda con las entradas de datos de streaming</span><span class="sxs-lookup"><span data-stu-id="14de3-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="14de3-149">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="14de3-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="14de3-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14de3-150">Next steps</span></span>
* [<span data-ttu-id="14de3-151">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="14de3-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="14de3-152">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14de3-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="14de3-153">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="14de3-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="14de3-154">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="14de3-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="14de3-155">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="14de3-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

