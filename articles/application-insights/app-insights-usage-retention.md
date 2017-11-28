---
title: "análisis de retención de aaaUser para aplicaciones web con Azure Application Insights | Documentos de Microsoft"
description: "¿Cuántos usuarios devuelven tooyour aplicación?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="9c349-103">Análisis de retención de usuarios para aplicaciones web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="9c349-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="9c349-104">característica de retención de Hello en [Azure Application Insights](app-insights-overview.md) le ayuda a analizar el número de usuarios devolver tooyour aplicación, y con qué frecuencia realizar determinadas tareas o lograr objetivos.</span><span class="sxs-lookup"><span data-stu-id="9c349-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="9c349-105">Por ejemplo, si ejecuta un sitio de juego, podría comparar números Hola de usuarios que devuelven toohello sitio después de perder un juego con número de Hola que devuelven después el ganador.</span><span class="sxs-lookup"><span data-stu-id="9c349-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="9c349-106">Esta información puede ayudarlo a mejorar la experiencia de los usuarios y la estrategia empresarial.</span><span class="sxs-lookup"><span data-stu-id="9c349-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="9c349-107">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="9c349-107">Get started</span></span>

<span data-ttu-id="9c349-108">Si aún no ve los datos en la herramienta de retención de hello en el portal de Application Insights hello, [Obtenga información acerca de cómo tooget a trabajar con herramientas de uso de hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c349-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="9c349-109">herramienta de retención de Hola</span><span class="sxs-lookup"><span data-stu-id="9c349-109">hello Retention tool</span></span>

![Herramienta Retención](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="9c349-111">barra de herramientas de Hello permite a los usuarios toocreate nuevos informes de retención, abra los informes existentes de retención, guardar el informe de retención actual o guardar como, revertir los cambios realizados toosaved informes, actualizar los datos en hello informe, recurso compartido a través de correo electrónico o vínculo directo y Hola de acceso página de documentación.</span><span class="sxs-lookup"><span data-stu-id="9c349-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="9c349-112">De forma predeterminada, la herramienta de retención muestra todos los usuarios que hicieron algo y que , posteriormente, regresaron e hicieron algo más a lo largo de un período.</span><span class="sxs-lookup"><span data-stu-id="9c349-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="9c349-113">Puede seleccionar una combinación diferente de eventos toonarrow Hola se centran en las actividades de usuario específico.</span><span class="sxs-lookup"><span data-stu-id="9c349-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="9c349-114">Agregue uno o varios filtros en las propiedades.</span><span class="sxs-lookup"><span data-stu-id="9c349-114">Add one or more filters on properties.</span></span> <span data-ttu-id="9c349-115">Por ejemplo, puede centrarse en los usuarios de un país o una región determinados.</span><span class="sxs-lookup"><span data-stu-id="9c349-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="9c349-116">Haga clic en **actualización** después de establecer filtros de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c349-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="9c349-117">Hello general retención gráfico muestra un resumen de retención del usuario a través de hello período de tiempo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9c349-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="9c349-118">cuadrícula de Hello muestra número Hola de usuarios conserva correspondiente generador de consultas de toohello de #2.</span><span class="sxs-lookup"><span data-stu-id="9c349-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="9c349-119">Cada fila representa un grupo de edad de los usuarios que llevó a cabo cualquier evento de hello período de tiempo mostrado.</span><span class="sxs-lookup"><span data-stu-id="9c349-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="9c349-120">Cada celda de la fila de hello muestra cuántas de ese grupo de edad devuelve al menos una vez en un período más adelante.</span><span class="sxs-lookup"><span data-stu-id="9c349-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="9c349-121">Algunos usuarios pueden regresar en más de un periodo.</span><span class="sxs-lookup"><span data-stu-id="9c349-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="9c349-122">tarjetas de información de Hello muestran los cinco eventos superiores iniciadores y cinco superior devuelve a los usuarios de eventos toogive una mejor comprensión de su informe de retención.</span><span class="sxs-lookup"><span data-stu-id="9c349-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Mantener el puntero sobre la retención](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="9c349-124">Los usuarios pueden desplazar el puntero sobre las celdas de botón de análisis de hello retención herramienta tooaccess hello y significa que explique qué celda Hola información sobre herramientas.</span><span class="sxs-lookup"><span data-stu-id="9c349-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="9c349-125">botón de análisis de Hello toma la herramienta de análisis de los usuarios toohello con un toogenerate consultar rellena automáticamente a los usuarios de celda Hola.</span><span class="sxs-lookup"><span data-stu-id="9c349-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="9c349-126">Utilizar la retención de tootrack de eventos empresariales</span><span class="sxs-lookup"><span data-stu-id="9c349-126">Use business events tootrack retention</span></span>

<span data-ttu-id="9c349-127">tooget hello más útil retención análisis, eventos de medida que representan actividades empresariales importantes.</span><span class="sxs-lookup"><span data-stu-id="9c349-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="9c349-128">Por ejemplo, muchos usuarios pueden abrir una página de la aplicación sin juego Hola que muestra.</span><span class="sxs-lookup"><span data-stu-id="9c349-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="9c349-129">Solo las vistas de página Hola de seguimiento, por tanto, proporcionaría una estimación inexacta de cuántas personas devuelven tooplay juego Hola después de se disfruta previamente.</span><span class="sxs-lookup"><span data-stu-id="9c349-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="9c349-130">tooget una imagen clara de devolver reproductores, la aplicación debe enviar un evento personalizado cuando se reproduce realmente a un usuario.</span><span class="sxs-lookup"><span data-stu-id="9c349-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="9c349-131">Es recomendable toocode los eventos personalizados que representan las acciones de la clave del negocio y usarlos para su análisis de retención.</span><span class="sxs-lookup"><span data-stu-id="9c349-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="9c349-132">resultado de juegos de hello toocapture, deberá toowrite una línea de código toosend una visión tooApplication de evento personalizado.</span><span class="sxs-lookup"><span data-stu-id="9c349-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="9c349-133">Si se escribe en el código de la página web de Hola o en Node.JS, parece similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="9c349-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="9c349-134">O en el código del servidor ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9c349-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="9c349-135">[Obtenga más información sobre la creación de eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="9c349-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c349-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c349-136">Next steps</span></span>
- <span data-ttu-id="9c349-137">uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="9c349-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="9c349-138">Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.</span><span class="sxs-lookup"><span data-stu-id="9c349-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="9c349-139">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="9c349-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="9c349-140">Embudos</span><span class="sxs-lookup"><span data-stu-id="9c349-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="9c349-141">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="9c349-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="9c349-142">Libros</span><span class="sxs-lookup"><span data-stu-id="9c349-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="9c349-143">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="9c349-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


