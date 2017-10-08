---
title: "aaaAzure modelo de datos de telemetría de aplicación visión - métrica de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de métricas"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="b9b80-103">Telemetría de métricas: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="b9b80-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="b9b80-104">Hay dos tipos de telemetría de métricas compatibles con [Application Insights](app-insights-overview.md): la medida única y la métrica previamente agregada.</span><span class="sxs-lookup"><span data-stu-id="b9b80-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="b9b80-105">La medida única es simplemente un nombre y un valor.</span><span class="sxs-lookup"><span data-stu-id="b9b80-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="b9b80-106">Métrica previamente agregado especifica un valor mínimo y máximo de métrica de hello en el intervalo de agregación de Hola y desviación estándar del mismo.</span><span class="sxs-lookup"><span data-stu-id="b9b80-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="b9b80-107">La telemetría de métricas previamente agregadas da por supuesto que el período de agregación es de un minuto.</span><span class="sxs-lookup"><span data-stu-id="b9b80-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="b9b80-108">Hay varios nombres de métrica conocidos compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b9b80-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="b9b80-109">Métricas que representan los contadores del sistema y de procesos:</span><span class="sxs-lookup"><span data-stu-id="b9b80-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="b9b80-110">**Nombre de .NET**</span><span class="sxs-lookup"><span data-stu-id="b9b80-110">**.NET name**</span></span>             | <span data-ttu-id="b9b80-111">**Nombre independiente de la plataforma**</span><span class="sxs-lookup"><span data-stu-id="b9b80-111">**Platform agnostic name**</span></span> | <span data-ttu-id="b9b80-112">**Nombre de API DE REST**</span><span class="sxs-lookup"><span data-stu-id="b9b80-112">**REST API name**</span></span> | <span data-ttu-id="b9b80-113">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="b9b80-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="b9b80-114">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-114">Work in progress...</span></span> | [<span data-ttu-id="b9b80-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="b9b80-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="b9b80-116">CPU total del equipo</span><span class="sxs-lookup"><span data-stu-id="b9b80-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="b9b80-117">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-117">Work in progress...</span></span> | [<span data-ttu-id="b9b80-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="b9b80-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="b9b80-119">memoria disponible en disco</span><span class="sxs-lookup"><span data-stu-id="b9b80-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="b9b80-120">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-120">Work in progress...</span></span> | [<span data-ttu-id="b9b80-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="b9b80-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="b9b80-122">CPU del proceso de hello hospeda aplicación hello</span><span class="sxs-lookup"><span data-stu-id="b9b80-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="b9b80-123">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-123">Work in progress...</span></span> | [<span data-ttu-id="b9b80-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="b9b80-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="b9b80-125">memoria utilizada por el proceso de Hola que se hospeda la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="b9b80-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="b9b80-126">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-126">Work in progress...</span></span> | [<span data-ttu-id="b9b80-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="b9b80-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="b9b80-128">tasa de operaciones de E/S se ejecuta por proceso que hospeda la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="b9b80-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="b9b80-129">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-129">Work in progress...</span></span> | [<span data-ttu-id="b9b80-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="b9b80-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="b9b80-131">tasa de solicitudes procesadas por la aplicación</span><span class="sxs-lookup"><span data-stu-id="b9b80-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="b9b80-132">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-132">Work in progress...</span></span> | [<span data-ttu-id="b9b80-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="b9b80-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="b9b80-134">velocidad de las excepciones producidas por la aplicación</span><span class="sxs-lookup"><span data-stu-id="b9b80-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="b9b80-135">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-135">Work in progress...</span></span> | [<span data-ttu-id="b9b80-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="b9b80-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="b9b80-137">tiempo medio de ejecución de solicitudes</span><span class="sxs-lookup"><span data-stu-id="b9b80-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="b9b80-138">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="b9b80-138">Work in progress...</span></span> | [<span data-ttu-id="b9b80-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="b9b80-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="b9b80-140">número de peticiones en espera de hello en una cola de procesamiento</span><span class="sxs-lookup"><span data-stu-id="b9b80-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="b9b80-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="b9b80-141">Name</span></span>

<span data-ttu-id="b9b80-142">Nombre de métrica de hello le gustaría toosee en el portal de Application Insights y la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="b9b80-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="b9b80-143">Valor</span><span class="sxs-lookup"><span data-stu-id="b9b80-143">Value</span></span>

<span data-ttu-id="b9b80-144">Valor único para la medida.</span><span class="sxs-lookup"><span data-stu-id="b9b80-144">Single value for measurement.</span></span> <span data-ttu-id="b9b80-145">Suma de las mediciones individuales para la agregación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9b80-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="b9b80-146">Recuento</span><span class="sxs-lookup"><span data-stu-id="b9b80-146">Count</span></span>

<span data-ttu-id="b9b80-147">Peso métrico de hello agrega métrica.</span><span class="sxs-lookup"><span data-stu-id="b9b80-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="b9b80-148">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="b9b80-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="b9b80-149">Min</span><span class="sxs-lookup"><span data-stu-id="b9b80-149">Min</span></span>

<span data-ttu-id="b9b80-150">Valor mínimo de hello agrega métrica.</span><span class="sxs-lookup"><span data-stu-id="b9b80-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="b9b80-151">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="b9b80-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="b9b80-152">max</span><span class="sxs-lookup"><span data-stu-id="b9b80-152">Max</span></span>

<span data-ttu-id="b9b80-153">Valor máximo de hello agrega métrica.</span><span class="sxs-lookup"><span data-stu-id="b9b80-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="b9b80-154">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="b9b80-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="b9b80-155">Desviación estándar</span><span class="sxs-lookup"><span data-stu-id="b9b80-155">Standard deviation</span></span>

<span data-ttu-id="b9b80-156">Desviación estándar de hello agrega métrica.</span><span class="sxs-lookup"><span data-stu-id="b9b80-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="b9b80-157">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="b9b80-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="b9b80-158">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="b9b80-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="b9b80-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9b80-159">Next steps</span></span>

- <span data-ttu-id="b9b80-160">Obtenga información acerca de cómo toouse [API de visión de la aplicación para eventos personalizados y las métricas](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="b9b80-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="b9b80-161">Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b9b80-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="b9b80-162">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b9b80-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
