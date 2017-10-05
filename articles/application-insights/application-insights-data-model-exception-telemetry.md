---
title: "Modelo de datos de telemetría de Azure Application Insights: telemetría de excepciones | Microsoft Docs"
description: "Modelo de datos de Application Insights para la telemetría de excepciones"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="6c3d1-103">Telemetría de excepciones: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="6c3d1-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="6c3d1-104">En [Application Insights](app-insights-overview.md), una instancia de Exception representa una excepción controlada o no controlada que se produjo durante la ejecución de la aplicación supervisada.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="6c3d1-105">Identificador del problema</span><span class="sxs-lookup"><span data-stu-id="6c3d1-105">Problem Id</span></span>

<span data-ttu-id="6c3d1-106">Identificador de dónde se produjo la excepción en el código.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="6c3d1-107">Se usa para el agrupamiento de las excepciones.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-107">Used for exceptions grouping.</span></span> <span data-ttu-id="6c3d1-108">Normalmente es una combinación del tipo de excepción y una función de la pila de llamadas.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="6c3d1-109">Longitud máxima: 1024 caracteres</span><span class="sxs-lookup"><span data-stu-id="6c3d1-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="6c3d1-110">Nivel de gravedad</span><span class="sxs-lookup"><span data-stu-id="6c3d1-110">Severity level</span></span>

<span data-ttu-id="6c3d1-111">El nivel de gravedad del seguimiento.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-111">Trace severity level.</span></span> <span data-ttu-id="6c3d1-112">El valor puede ser `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="6c3d1-113">Detalles de la excepción</span><span class="sxs-lookup"><span data-stu-id="6c3d1-113">Exception details</span></span>

<span data-ttu-id="6c3d1-114">(Se ampliará)</span><span class="sxs-lookup"><span data-stu-id="6c3d1-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="6c3d1-115">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="6c3d1-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="6c3d1-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="6c3d1-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="6c3d1-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c3d1-117">Next steps</span></span>

- <span data-ttu-id="6c3d1-118">Vea [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="6c3d1-119">Obtenga información para el [diagnóstico de excepciones en aplicaciones web con Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="6c3d1-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="6c3d1-120">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c3d1-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
