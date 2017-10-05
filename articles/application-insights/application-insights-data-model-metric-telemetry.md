---
title: "Modelo de datos de telemetría de Azure Application Insights: telemetría de métricas | Microsoft Docs"
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
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="7cd5b-103">Telemetría de métricas: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="7cd5b-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="7cd5b-104">Hay dos tipos de telemetría de métricas compatibles con [Application Insights](app-insights-overview.md): la medida única y la métrica previamente agregada.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="7cd5b-105">La medida única es simplemente un nombre y un valor.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="7cd5b-106">La métrica previamente agregada especifica el valor mínimo y máximo de la métrica en el intervalo de agregación y la desviación estándar del mismo.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="7cd5b-107">La telemetría de métricas previamente agregadas da por supuesto que el período de agregación es de un minuto.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="7cd5b-108">Hay varios nombres de métrica conocidos compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="7cd5b-109">Métricas que representan los contadores del sistema y de procesos:</span><span class="sxs-lookup"><span data-stu-id="7cd5b-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="7cd5b-110">**Nombre de .NET**</span><span class="sxs-lookup"><span data-stu-id="7cd5b-110">**.NET name**</span></span>             | <span data-ttu-id="7cd5b-111">**Nombre independiente de la plataforma**</span><span class="sxs-lookup"><span data-stu-id="7cd5b-111">**Platform agnostic name**</span></span> | <span data-ttu-id="7cd5b-112">**Nombre de API DE REST**</span><span class="sxs-lookup"><span data-stu-id="7cd5b-112">**REST API name**</span></span> | <span data-ttu-id="7cd5b-113">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="7cd5b-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="7cd5b-114">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-114">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="7cd5b-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="7cd5b-116">CPU total del equipo</span><span class="sxs-lookup"><span data-stu-id="7cd5b-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="7cd5b-117">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-117">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="7cd5b-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="7cd5b-119">memoria disponible en disco</span><span class="sxs-lookup"><span data-stu-id="7cd5b-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="7cd5b-120">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-120">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="7cd5b-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="7cd5b-122">CPU del proceso que hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd5b-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="7cd5b-123">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-123">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="7cd5b-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="7cd5b-125">memoria que usa el proceso que hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd5b-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="7cd5b-126">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-126">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="7cd5b-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="7cd5b-128">tasa de operaciones de E/S ejecutadas por el proceso que hospeda la aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd5b-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="7cd5b-129">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-129">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="7cd5b-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="7cd5b-131">tasa de solicitudes procesadas por la aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd5b-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="7cd5b-132">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-132">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="7cd5b-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="7cd5b-134">velocidad de las excepciones producidas por la aplicación</span><span class="sxs-lookup"><span data-stu-id="7cd5b-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="7cd5b-135">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-135">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="7cd5b-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="7cd5b-137">tiempo medio de ejecución de solicitudes</span><span class="sxs-lookup"><span data-stu-id="7cd5b-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="7cd5b-138">Trabajo en curso...</span><span class="sxs-lookup"><span data-stu-id="7cd5b-138">Work in progress...</span></span> | [<span data-ttu-id="7cd5b-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="7cd5b-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="7cd5b-140">número de peticiones en espera de procesamiento en una cola</span><span class="sxs-lookup"><span data-stu-id="7cd5b-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="7cd5b-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="7cd5b-141">Name</span></span>

<span data-ttu-id="7cd5b-142">El nombre de la métrica que le gustaría ver en el portal de Application Insights y la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="7cd5b-143">Valor</span><span class="sxs-lookup"><span data-stu-id="7cd5b-143">Value</span></span>

<span data-ttu-id="7cd5b-144">Valor único para la medida.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-144">Single value for measurement.</span></span> <span data-ttu-id="7cd5b-145">Suma de las mediciones individuales para la agregación.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="7cd5b-146">Recuento</span><span class="sxs-lookup"><span data-stu-id="7cd5b-146">Count</span></span>

<span data-ttu-id="7cd5b-147">Peso de la métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="7cd5b-148">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="7cd5b-149">Min</span><span class="sxs-lookup"><span data-stu-id="7cd5b-149">Min</span></span>

<span data-ttu-id="7cd5b-150">Valor mínimo de la métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="7cd5b-151">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="7cd5b-152">max</span><span class="sxs-lookup"><span data-stu-id="7cd5b-152">Max</span></span>

<span data-ttu-id="7cd5b-153">Valor máximo de la métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="7cd5b-154">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="7cd5b-155">Desviación estándar</span><span class="sxs-lookup"><span data-stu-id="7cd5b-155">Standard deviation</span></span>

<span data-ttu-id="7cd5b-156">Desviación estándar de la métrica agregada.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="7cd5b-157">No se debe establecer para una medida.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="7cd5b-158">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="7cd5b-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="7cd5b-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7cd5b-159">Next steps</span></span>

- <span data-ttu-id="7cd5b-160">Obtenga información sobre cómo usar la [API de Application Insights para eventos y métricas personalizados](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="7cd5b-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="7cd5b-161">Consulte el [modelo de datos](application-insights-data-model.md) para ver los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="7cd5b-162">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7cd5b-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
