---
title: "aaaAzure modelos de datos de telemetría de aplicación visión, evento de telemetría | Documentos de Microsoft"
description: "Modelo de datos de Application Insights para la telemetría de eventos"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="5112e-103">Telemetría de eventos: modelo de datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="5112e-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="5112e-104">Puede crear eventos de elementos de telemetría (en [Application Insights](app-insights-overview.md)) toorepresent un evento producido en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5112e-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="5112e-105">Normalmente es una interacción del usuario como un clic de botón o la desprotección de un pedido.</span><span class="sxs-lookup"><span data-stu-id="5112e-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="5112e-106">También puede ser un evento de ciclo de vida de la aplicación como la actualización de la inicialización o la configuración.</span><span class="sxs-lookup"><span data-stu-id="5112e-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="5112e-107">Semánticamente, eventos pueden o no ser toorequests correlacionados.</span><span class="sxs-lookup"><span data-stu-id="5112e-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="5112e-108">Pero si se usa correctamente, la telemetría de eventos es más importante que las solicitudes o los seguimientos.</span><span class="sxs-lookup"><span data-stu-id="5112e-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="5112e-109">Eventos representan la telemetría de negocio y debe ser un tooseparate asunto, menos agresiva [muestreo](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="5112e-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="5112e-110">Nombre</span><span class="sxs-lookup"><span data-stu-id="5112e-110">Name</span></span>

<span data-ttu-id="5112e-111">Nombre del evento.</span><span class="sxs-lookup"><span data-stu-id="5112e-111">Event name.</span></span> <span data-ttu-id="5112e-112">agrupación adecuada tooallow y métricas útiles, restringir la aplicación para que genere un pequeño número de nombres de evento independiente.</span><span class="sxs-lookup"><span data-stu-id="5112e-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="5112e-113">Por ejemplo, no utilice un nombre diferente para cada instancia generada de un evento.</span><span class="sxs-lookup"><span data-stu-id="5112e-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="5112e-114">Longitud máxima: 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="5112e-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="5112e-115">Propiedades personalizadas</span><span class="sxs-lookup"><span data-stu-id="5112e-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="5112e-116">Medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="5112e-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="5112e-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5112e-117">Next steps</span></span>

- <span data-ttu-id="5112e-118">Consulte el [modelo de datos](application-insights-data-model.md) para ver los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5112e-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="5112e-119">Escritura de telemetría de eventos personalizada</span><span class="sxs-lookup"><span data-stu-id="5112e-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="5112e-120">Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5112e-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
