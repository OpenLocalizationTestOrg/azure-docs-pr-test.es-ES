---
title: "aaaHow tooconfigure datos salidas para trabajos de análisis de transmisiones | Documentos de Microsoft"
description: "Configuración de salidas de datos para trabajos de Análisis de transmisiones | segmento de ruta de aprendizaje."
keywords: salida de datos, movimiento de datos
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="940ee-104">¿Cómo tooconfigure datos salidas para trabajos de análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="940ee-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="940ee-105">Trabajos de análisis de transmisiones de Azure pueden ser tooone conectado o más salidas de datos, que definen un receptor de datos de conexión tooan existente.</span><span class="sxs-lookup"><span data-stu-id="940ee-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="940ee-106">Como el trabajo de análisis de transmisiones procesa y transforma los datos entrantes, una secuencia de eventos de salida de datos se escribe la salida del trabajo tooyour.</span><span class="sxs-lookup"><span data-stu-id="940ee-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="940ee-107">Salidas de flujo de datos de análisis pueden ser paneles en tiempo real de toosource usado o alertas, flujos de trabajo de movimiento de datos de desencadenador o simplemente archivar datos de procesamiento por lotes más adelante.</span><span class="sxs-lookup"><span data-stu-id="940ee-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="940ee-108">El Análisis de transmisiones tiene una integración de primera clase con varios servicios de Azure, que se documentan aquí con detalle.</span><span class="sxs-lookup"><span data-stu-id="940ee-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="940ee-109">un trabajo de análisis de transmisiones de salida tooyour tooadd:</span><span class="sxs-lookup"><span data-stu-id="940ee-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="940ee-110">Hola [portal de Azure](https://portal.azure.com), abra el trabajo y haga clic en **salidas** y, a continuación, haga clic en **agregar** en la hoja de salidas de Hola que aparece.</span><span class="sxs-lookup"><span data-stu-id="940ee-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Agregar salidas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="940ee-112">Proporcione un nombre descriptivo para esta salida de hello **Alias de salida** cuadro.</span><span class="sxs-lookup"><span data-stu-id="940ee-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="940ee-113">Este nombre se puede utilizar en consultas de la tarea más adelante en la salida de toohello de toorefer.</span><span class="sxs-lookup"><span data-stu-id="940ee-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="940ee-114">Rellene el resto de Hola de hello requerido conexión propiedades tooconnect tooyour salida.</span><span class="sxs-lookup"><span data-stu-id="940ee-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="940ee-115">Estos campos varían según el tipo de salida y se definen en detalle aquí.</span><span class="sxs-lookup"><span data-stu-id="940ee-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Elección del tipo de movimiento de datos](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="940ee-117">Según el tipo de salida de hello, puede que necesite toospecify cómo Hola se serializa o con formato.</span><span class="sxs-lookup"><span data-stu-id="940ee-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="940ee-118">configuración de serialización específico de Hola para cada tipo de salida se documenta aquí.</span><span class="sxs-lookup"><span data-stu-id="940ee-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="940ee-119">Rellene el resto de Hola Hola conexión necesaria propiedades tooconnect tooyour del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="940ee-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="940ee-120">Estos campos varían según el tipo de entrada y origen y se definen en detalle en hello [artículo Crear trabajo](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="940ee-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="940ee-121">Cualquier trabajo toohello agregada del elemento de salida, debe existir antes de inicia el trabajo de Hola y eventos de inicio del flujo.</span><span class="sxs-lookup"><span data-stu-id="940ee-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="940ee-122">Por ejemplo, si utiliza almacenamiento de blobs como salida, el trabajo de hello no creará una cuenta de almacenamiento automáticamente.</span><span class="sxs-lookup"><span data-stu-id="940ee-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="940ee-123">Debe toobe creada por el usuario de hello antes de iniciarse el trabajo de hello ASA.</span><span class="sxs-lookup"><span data-stu-id="940ee-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="940ee-124">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="940ee-124">Get help</span></span>
<span data-ttu-id="940ee-125">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="940ee-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="940ee-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="940ee-126">Next steps</span></span>
* [<span data-ttu-id="940ee-127">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="940ee-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="940ee-128">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="940ee-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="940ee-129">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="940ee-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="940ee-130">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="940ee-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="940ee-131">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="940ee-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

