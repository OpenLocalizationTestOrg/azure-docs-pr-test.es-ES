---
title: 'Servicio de aplicaciones de Azure: escalado de aplicaciones de Servicio de aplicaciones'
description: "Obtenga información acerca de hello pormenores de escalar la aplicación de servicio de aplicaciones."
keywords: servicio de aplicaciones, servicio de aplicaciones de azure, escala, escalable, plan del servicio de aplicaciones, costo del servicio de aplicaciones
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="eb276-104">Servicio de aplicaciones de Azure: escalado de aplicaciones de Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="eb276-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="eb276-105">Las aplicaciones hospedadas en el Servicio de aplicaciones de Azure pueden [alcanzar una escala enorme](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="eb276-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="eb276-106">Sin embargo, el escalado de una aplicación es un problema complejo que no tiene una solución de "talla única".</span><span class="sxs-lookup"><span data-stu-id="eb276-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="eb276-107">toocorrectly escalar la aplicación 3 áreas clave que contribuyen al éxito de las aplicaciones de tooyour:</span><span class="sxs-lookup"><span data-stu-id="eb276-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="eb276-108">Comprensión de la arquitectura de la aplicación y sus puntos débiles.</span><span class="sxs-lookup"><span data-stu-id="eb276-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="eb276-109">¿Se trata de una aplicación con estado?</span><span class="sxs-lookup"><span data-stu-id="eb276-109">Is your Application Stateful?</span></span> <span data-ttu-id="eb276-110">¿O sin estado?</span><span class="sxs-lookup"><span data-stu-id="eb276-110">Stateless?</span></span>
   * <span data-ttu-id="eb276-111">¿Cuáles son todos los componentes de hello de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="eb276-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="eb276-112">¿Dónde están los cuellos de botella de hello en la aplicación hello?</span><span class="sxs-lookup"><span data-stu-id="eb276-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="eb276-113">Cuando la carga es aplicación tooyour aplicado, ¿qué interrumpirá la primera?</span><span class="sxs-lookup"><span data-stu-id="eb276-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="eb276-114">Hola descripción espera que los requisitos de carga y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="eb276-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="eb276-115">¿Necesita aplicación hello tooserve mil usuarios? ¿o un millón?</span><span class="sxs-lookup"><span data-stu-id="eb276-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="eb276-116">¿Procederá el tráfico de una sola ubicación geográfica o será global?</span><span class="sxs-lookup"><span data-stu-id="eb276-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="eb276-117">¿Hay variaciones estacionales? ¿Picos de tráfico?</span><span class="sxs-lookup"><span data-stu-id="eb276-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="eb276-118">¿Con qué rapidez debe responder aplicación hello?</span><span class="sxs-lookup"><span data-stu-id="eb276-118">How fast should hello app respond?</span></span> <span data-ttu-id="eb276-119">¿Un segundo?</span><span class="sxs-lookup"><span data-stu-id="eb276-119">1 second?</span></span> <span data-ttu-id="eb276-120">¿Un milisegundo?</span><span class="sxs-lookup"><span data-stu-id="eb276-120">1 millisecond?</span></span>
3. <span data-ttu-id="eb276-121">Descripción correctamente Aproveche Hola plataforma y la aplicación de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="eb276-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="eb276-122">¿Qué características deben aprovechar tooachieve mis objetivos de escala?</span><span class="sxs-lookup"><span data-stu-id="eb276-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="eb276-123">Esta sección le ayudará a comprender todos los factores de Hola y ayuda idear una estrategia que aprovecha las ventajas de hello tooachieve de características de servicio de aplicaciones necesario los objetivos de escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="eb276-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

