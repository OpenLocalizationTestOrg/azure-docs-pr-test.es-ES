---
title: "toostart aaaHow los trabajos de análisis de transmisiones de streaming | Documentos de Microsoft"
description: "Ejecución de un trabajo de streaming en Análisis de transmisiones de Azure | segmento de ruta de acceso de aprendizaje."
keywords: Trabajos de streaming
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="d5b21-104">¿Cómo toorun una transmisión por secuencias de trabajo de análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d5b21-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="d5b21-105">Cuando un trabajo de entrada, consulta y resultado todas se han especificado que puede iniciar trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b21-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="d5b21-106">toostart el trabajo:</span><span class="sxs-lookup"><span data-stu-id="d5b21-106">toostart your job:</span></span>

1. <span data-ttu-id="d5b21-107">En el portal de Azure clásico de hello, en el panel de trabajo de hello, haga clic en **iniciar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b21-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Botón Iniciar trabajo](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="d5b21-109">Hola portal de Azure, haga clic en **iniciar** al principio de hello de la página de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d5b21-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Botón Iniciar trabajo de Azure Portal](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="d5b21-111">Especifique un **iniciar salida** valor toodetermine al trabajo comenzará a producir un resultado.</span><span class="sxs-lookup"><span data-stu-id="d5b21-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="d5b21-112">Hello configuración predeterminada para los trabajos que no se ha iniciado previamente es **hora de inicio del trabajo**, lo que significa que el trabajo de hello inmediatamente comenzará a procesar los datos.</span><span class="sxs-lookup"><span data-stu-id="d5b21-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="d5b21-113">También puede especificar un **personalizado** tiempo Hola pasado (para consumir datos históricos) o hello futura (toodelay procesamiento hasta una fecha futura).</span><span class="sxs-lookup"><span data-stu-id="d5b21-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="d5b21-114">Para casos en que se ha iniciado y detenido, previamente un trabajo Hola opción **última hora de detención** está disponible en el trabajo de hello tooresume de orden de última hora de salida de hello y evitar la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="d5b21-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Hora de inicio del trabajo de streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Hora de inicio del trabajo de streaming de Azure Portal](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="d5b21-117">Confirme la selección.</span><span class="sxs-lookup"><span data-stu-id="d5b21-117">Confirm your selection.</span></span> <span data-ttu-id="d5b21-118">estado del trabajo Hola cambiará demasiado*iniciando* y en breve se moverán demasiado*ejecutando* una vez que ha iniciado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b21-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="d5b21-119">Puede supervisar el progreso de Hola de hello **iniciar** operación Hola **centro de notificaciones**:</span><span class="sxs-lookup"><span data-stu-id="d5b21-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![progreso del trabajo de streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Progreso del trabajo de streaming de Azure Portal](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="d5b21-122">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="d5b21-122">Get help</span></span>
<span data-ttu-id="d5b21-123">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="d5b21-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5b21-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5b21-124">Next steps</span></span>
* [<span data-ttu-id="d5b21-125">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="d5b21-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d5b21-126">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d5b21-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d5b21-127">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d5b21-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d5b21-128">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d5b21-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d5b21-129">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d5b21-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

