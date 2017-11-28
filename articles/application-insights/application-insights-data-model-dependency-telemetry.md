---
title: "aaaAzure modelo de datos de telemetría de aplicación visión - dependencia telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de dependencias"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="3da70-103">Telemetría de dependencias: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="3da70-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="3da70-104">Telemetría de dependencia (en [Application Insights](app-insights-overview.md)) representa una interacción del componente de hello supervisado con un componente remoto como SQL o un extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="3da70-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="3da70-105">Nombre</span><span class="sxs-lookup"><span data-stu-id="3da70-105">Name</span></span>

<span data-ttu-id="3da70-106">Nombre del comando de hello iniciada con esta llamada de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3da70-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="3da70-107">Valor de cardinalidad bajo.</span><span class="sxs-lookup"><span data-stu-id="3da70-107">Low cardinality value.</span></span> <span data-ttu-id="3da70-108">Algunos ejemplos son el nombre del procedimiento almacenado y la plantilla de ruta de acceso de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="3da70-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="3da70-109">ID</span><span class="sxs-lookup"><span data-stu-id="3da70-109">ID</span></span>

<span data-ttu-id="3da70-110">Identificador de una instancia de llamada de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3da70-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="3da70-111">Se utiliza para la correlación con elemento de telemetría de solicitud de hello correspondiente toothis dependencia llamada.</span><span class="sxs-lookup"><span data-stu-id="3da70-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="3da70-112">Para obtener más información, vea la página de [correlación](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="3da70-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="3da70-113">Datos</span><span class="sxs-lookup"><span data-stu-id="3da70-113">Data</span></span>

<span data-ttu-id="3da70-114">Comando iniciado por esta llamada de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3da70-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="3da70-115">Algunos ejemplos son la instrucción SQL y la dirección URL HTTP con todos los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="3da70-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="3da70-116">Tipo</span><span class="sxs-lookup"><span data-stu-id="3da70-116">Type</span></span>

<span data-ttu-id="3da70-117">Nombre del tipo de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3da70-117">Dependency type name.</span></span> <span data-ttu-id="3da70-118">Valor de cardinalidad bajo para una agrupación lógica de dependencias y la interpretación de otros campos como commandName y resultCode.</span><span class="sxs-lookup"><span data-stu-id="3da70-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="3da70-119">Algunos ejemplos son SQL, tabla de Azure y HTTP.</span><span class="sxs-lookup"><span data-stu-id="3da70-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="3da70-120">Destino</span><span class="sxs-lookup"><span data-stu-id="3da70-120">Target</span></span>

<span data-ttu-id="3da70-121">Sitio de destino de una llamada de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3da70-121">Target site of a dependency call.</span></span> <span data-ttu-id="3da70-122">Algunos ejemplos son el nombre del servidor y la dirección de host.</span><span class="sxs-lookup"><span data-stu-id="3da70-122">Examples are server name, host address.</span></span> <span data-ttu-id="3da70-123">Para más información, vea la página de [correlación](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="3da70-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="3da70-124">Duración</span><span class="sxs-lookup"><span data-stu-id="3da70-124">Duration</span></span>

<span data-ttu-id="3da70-125">Duración de la solicitud en formato: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="3da70-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="3da70-126">Debe ser menor de `1000` días.</span><span class="sxs-lookup"><span data-stu-id="3da70-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="3da70-127">Código de resultado</span><span class="sxs-lookup"><span data-stu-id="3da70-127">Result code</span></span>

<span data-ttu-id="3da70-128">Código de resultado de una llamada de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3da70-128">Result code of a dependency call.</span></span> <span data-ttu-id="3da70-129">Algunos ejemplos son el código de error SQL y el código de estado HTTP.</span><span class="sxs-lookup"><span data-stu-id="3da70-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="3da70-130">Correcto</span><span class="sxs-lookup"><span data-stu-id="3da70-130">Success</span></span>

<span data-ttu-id="3da70-131">Indicación de si la llamada es correcta o no.</span><span class="sxs-lookup"><span data-stu-id="3da70-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="3da70-132">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="3da70-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="3da70-133">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="3da70-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="3da70-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3da70-134">Next steps</span></span>

- <span data-ttu-id="3da70-135">Configure el seguimiento de dependencias para [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="3da70-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="3da70-136">Configure el seguimiento de dependencias para [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="3da70-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="3da70-137">Escritura de una telemetría de dependencia personalizada</span><span class="sxs-lookup"><span data-stu-id="3da70-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="3da70-138">Consulte el [modelo de datos](application-insights-data-model.md) para ver los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3da70-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3da70-139">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3da70-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
