---
title: "aaaAzure modelo de datos de telemetría de aplicación visión - seguimiento de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de seguimientos"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="75d23-103">Telemetría de seguimientos: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="75d23-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="75d23-104">La telemetría de seguimientos (en [Application Insights](app-insights-overview.md)) representa instrucciones de seguimiento de estilo `printf` en las que se pueden realizar búsquedas de texto.</span><span class="sxs-lookup"><span data-stu-id="75d23-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="75d23-105">`Log4Net`, `NLog` y las demás entradas de archivo de registro basadas en texto se convierten a instancias de este tipo.</span><span class="sxs-lookup"><span data-stu-id="75d23-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="75d23-106">seguimiento de Hello no tiene medidas como una extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="75d23-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="75d23-107">Message</span><span class="sxs-lookup"><span data-stu-id="75d23-107">Message</span></span>

<span data-ttu-id="75d23-108">Mensaje de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="75d23-108">Trace message.</span></span>

<span data-ttu-id="75d23-109">Longitud máxima: 32 768 caracteres</span><span class="sxs-lookup"><span data-stu-id="75d23-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="75d23-110">Nivel de gravedad</span><span class="sxs-lookup"><span data-stu-id="75d23-110">Severity level</span></span>

<span data-ttu-id="75d23-111">El nivel de gravedad del seguimiento.</span><span class="sxs-lookup"><span data-stu-id="75d23-111">Trace severity level.</span></span> <span data-ttu-id="75d23-112">El valor puede ser `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="75d23-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="75d23-113">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="75d23-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="75d23-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75d23-114">Next steps</span></span>

- <span data-ttu-id="75d23-115">[Exploración de los registros de seguimiento de .NET en Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="75d23-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="75d23-116">[Exploración de los registros de seguimiento de Java en Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="75d23-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="75d23-117">Consulte el [modelo de datos](application-insights-data-model.md) para ver los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="75d23-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="75d23-118">Escritura de telemetría de seguimiento personalizada</span><span class="sxs-lookup"><span data-stu-id="75d23-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="75d23-119">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="75d23-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
