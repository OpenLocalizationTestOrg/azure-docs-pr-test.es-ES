---
title: "aaaAzure modelo de datos de telemetría de aplicación visión: excepción de telemetría | Documentos de Microsoft"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="f9017-103">Telemetría de excepciones: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9017-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="f9017-104">En [Application Insights](app-insights-overview.md), una instancia de excepción representa una excepción controlada o no controlada que se produjeron durante la ejecución de la aplicación hello supervisado.</span><span class="sxs-lookup"><span data-stu-id="f9017-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="f9017-105">Identificador del problema</span><span class="sxs-lookup"><span data-stu-id="f9017-105">Problem Id</span></span>

<span data-ttu-id="f9017-106">Identificador de donde se produjo la excepción de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="f9017-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="f9017-107">Se usa para el agrupamiento de las excepciones.</span><span class="sxs-lookup"><span data-stu-id="f9017-107">Used for exceptions grouping.</span></span> <span data-ttu-id="f9017-108">Normalmente es una combinación de tipo de excepción y una función de la pila de llamadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9017-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="f9017-109">Longitud máxima: 1024 caracteres</span><span class="sxs-lookup"><span data-stu-id="f9017-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="f9017-110">Nivel de gravedad</span><span class="sxs-lookup"><span data-stu-id="f9017-110">Severity level</span></span>

<span data-ttu-id="f9017-111">El nivel de gravedad del seguimiento.</span><span class="sxs-lookup"><span data-stu-id="f9017-111">Trace severity level.</span></span> <span data-ttu-id="f9017-112">El valor puede ser `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="f9017-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="f9017-113">Detalles de la excepción</span><span class="sxs-lookup"><span data-stu-id="f9017-113">Exception details</span></span>

<span data-ttu-id="f9017-114">(toobe extendido)</span><span class="sxs-lookup"><span data-stu-id="f9017-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="f9017-115">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="f9017-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="f9017-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="f9017-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="f9017-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9017-117">Next steps</span></span>

- <span data-ttu-id="f9017-118">Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9017-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="f9017-119">Obtenga información acerca de cómo demasiado[diagnosticar las excepciones en las aplicaciones web con Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="f9017-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="f9017-120">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f9017-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
