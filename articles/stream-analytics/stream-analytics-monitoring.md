---
title: "Supervisión de trabajo de análisis de transmisiones de aaaUnderstanding | Documentos de Microsoft"
description: "Descripción de la supervisión del trabajo de Análisis de transmisiones"
keywords: "supervisión de consultas"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="4cb9d-104">Comprender la supervisión de trabajo de análisis de transmisiones y cómo toomonitor consultas</span><span class="sxs-lookup"><span data-stu-id="4cb9d-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="4cb9d-105">Introducción: página Hola monitor</span><span class="sxs-lookup"><span data-stu-id="4cb9d-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="4cb9d-106">Hola ambos expuesta métricas de rendimiento clave que se pueden toomonitor usado y solucionar problemas de rendimiento de la consulta y el trabajo de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="4cb9d-107">toosee estas métricas, examinar está interesado en Ver hello de vista y las métricas para el trabajo de análisis de flujo de toohello **supervisión** sección en la página de información general de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Vínculo de supervisión](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="4cb9d-109">ventana Hello aparecerán como se muestra:</span><span class="sxs-lookup"><span data-stu-id="4cb9d-109">hello window will appear as shown:</span></span>

![Panel de supervisión de trabajos](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="4cb9d-111">Métricas disponibles para Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="4cb9d-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="4cb9d-112">Métrica</span><span class="sxs-lookup"><span data-stu-id="4cb9d-112">Metric</span></span>                 | <span data-ttu-id="4cb9d-113">Definición</span><span class="sxs-lookup"><span data-stu-id="4cb9d-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="4cb9d-114">SU % uso</span><span class="sxs-lookup"><span data-stu-id="4cb9d-114">SU % Utilization</span></span>       | <span data-ttu-id="4cb9d-115">uso de Hola de hello unidades de transmisión por secuencias asignados tooa trabajo Hola de ficha escala del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="4cb9d-116">Si este indicador llega o supera el 80 %, existe una gran probabilidad de que el procesamiento de eventos se retrase o deje de avanzar.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="4cb9d-117">Eventos de entrada</span><span class="sxs-lookup"><span data-stu-id="4cb9d-117">Input Events</span></span>           | <span data-ttu-id="4cb9d-118">Cantidad de datos recibidos por el trabajo de análisis de transmisiones de hello, en número de eventos.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="4cb9d-119">Esto puede ser usado toovalidate que se envían eventos de origen de entrada de toohello.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="4cb9d-120">Eventos de salida</span><span class="sxs-lookup"><span data-stu-id="4cb9d-120">Output Events</span></span>          | <span data-ttu-id="4cb9d-121">Cantidad de datos enviados por hello análisis de transmisiones trabajo toohello destino de salida, en número de eventos.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="4cb9d-122">Eventos que no funcionan</span><span class="sxs-lookup"><span data-stu-id="4cb9d-122">Out-of-Order Events</span></span>    | <span data-ttu-id="4cb9d-123">Número de eventos recibidos fuera de servicio que se anularon o tiene una marca de tiempo ajustada, basada en hello directiva de orden de eventos.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="4cb9d-124">Esto se puede ver afectado por la configuración de Hola de configuración de la ventana de tolerancia de fuera de lugar Hola.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="4cb9d-125">Errores de conversión de datos</span><span class="sxs-lookup"><span data-stu-id="4cb9d-125">Data Conversion Errors</span></span> | <span data-ttu-id="4cb9d-126">Número de errores de conversión de datos que produce un trabajo de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="4cb9d-127">Errores de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="4cb9d-127">Runtime Errors</span></span>         | <span data-ttu-id="4cb9d-128">número total de Hola de errores que se producen durante la ejecución de un trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="4cb9d-129">Eventos de entrada retrasada</span><span class="sxs-lookup"><span data-stu-id="4cb9d-129">Late Input Events</span></span>      | <span data-ttu-id="4cb9d-130">Número de eventos que llegan tarde desde el origen de Hola que ya se han eliminado o su marca de tiempo se ha ajustado, en función de la configuración de directiva de orden de eventos de Hola de tiempo de ejecución de tolerancia de llegada tardía Hola.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="4cb9d-131">Solicitudes de función</span><span class="sxs-lookup"><span data-stu-id="4cb9d-131">Function Requests</span></span>      | <span data-ttu-id="4cb9d-132">Número de llamadas toohello función de aprendizaje automático de Azure (si existe).</span><span class="sxs-lookup"><span data-stu-id="4cb9d-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="4cb9d-133">Solicitudes de función con errores</span><span class="sxs-lookup"><span data-stu-id="4cb9d-133">Failed Function Requests</span></span> | <span data-ttu-id="4cb9d-134">Número de llamadas a la función Azure Machine Learning con error (si corresponde).</span><span class="sxs-lookup"><span data-stu-id="4cb9d-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="4cb9d-135">Eventos de función</span><span class="sxs-lookup"><span data-stu-id="4cb9d-135">Function Events</span></span>        | <span data-ttu-id="4cb9d-136">Número de eventos enviados toohello función de aprendizaje automático de Azure (si existe).</span><span class="sxs-lookup"><span data-stu-id="4cb9d-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="4cb9d-137">Bytes del evento de entrada</span><span class="sxs-lookup"><span data-stu-id="4cb9d-137">Input Event Bytes</span></span>      | <span data-ttu-id="4cb9d-138">Cantidad de datos recibidos por trabajo de análisis de transmisiones de hello, en bytes.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="4cb9d-139">Esto puede ser usado toovalidate que se envían eventos de origen de entrada de toohello.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="4cb9d-140">Personalizar supervisión en el portal de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="4cb9d-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="4cb9d-141">Puede ajustar el tipo de gráfico de métricas que se muestran, Hola y el intervalo en la configuración de hello Editar gráfico de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4cb9d-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="4cb9d-142">Para obtener más información, consulte [cómo tooCustomize supervisión](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="4cb9d-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Escala de tiempo de supervisión de consultas](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="4cb9d-144">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="4cb9d-144">Get help</span></span>
<span data-ttu-id="4cb9d-145">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="4cb9d-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cb9d-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cb9d-146">Next steps</span></span>
* [<span data-ttu-id="4cb9d-147">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="4cb9d-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4cb9d-148">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4cb9d-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4cb9d-149">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="4cb9d-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4cb9d-150">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="4cb9d-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4cb9d-151">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4cb9d-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

