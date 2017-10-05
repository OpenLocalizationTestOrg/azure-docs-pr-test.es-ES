---
title: "Análisis de retención de usuarios para aplicaciones web con Azure Application Insights | Microsoft Docs"
description: "¿Cuántos usuarios regresan a la aplicación?"
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
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="1c772-103">Análisis de retención de usuarios para aplicaciones web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="1c772-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="1c772-104">La característica Retención de [Azure Application Insights](app-insights-overview.md) le ayuda a analizar cuántos usuarios regresan a la aplicación, y con qué frecuencia realizan determinadas tareas o logran objetivos.</span><span class="sxs-lookup"><span data-stu-id="1c772-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="1c772-105">Por ejemplo, si ejecuta un sitio de juegos, puede comparar el número de usuarios que regresan al sitio después de perder una partida con la cantidad que vuelven tras ganar.</span><span class="sxs-lookup"><span data-stu-id="1c772-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="1c772-106">Esta información puede ayudarlo a mejorar la experiencia de los usuarios y la estrategia empresarial.</span><span class="sxs-lookup"><span data-stu-id="1c772-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="1c772-107">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="1c772-107">Get started</span></span>

<span data-ttu-id="1c772-108">Si aún no ve los datos en la herramienta Retención del portal de Application Insights, [obtenga información sobre cómo empezar a trabajar con las herramientas de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c772-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="1c772-109">La herramienta Retención</span><span class="sxs-lookup"><span data-stu-id="1c772-109">The Retention tool</span></span>

![Herramienta Retención](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="1c772-111">La barra de herramientas permite a los usuarios crear nuevos informes de retención, abrir los informes ya existentes, guardar el informe de retención actual (o guardarlo mediante la opción Guardar como), revertir los cambios efectuados en los informes guardados, actualizar los datos del informe, compartir un informe por correo electrónico o vínculo directo y acceder a la página de documentación.</span><span class="sxs-lookup"><span data-stu-id="1c772-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="1c772-112">De forma predeterminada, la herramienta de retención muestra todos los usuarios que hicieron algo y que , posteriormente, regresaron e hicieron algo más a lo largo de un período.</span><span class="sxs-lookup"><span data-stu-id="1c772-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="1c772-113">Puede seleccionar una combinación diferente de eventos para centrar el enfoque en las actividades específicas del usuario.</span><span class="sxs-lookup"><span data-stu-id="1c772-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="1c772-114">Agregue uno o varios filtros en las propiedades.</span><span class="sxs-lookup"><span data-stu-id="1c772-114">Add one or more filters on properties.</span></span> <span data-ttu-id="1c772-115">Por ejemplo, puede centrarse en los usuarios de un país o una región determinados.</span><span class="sxs-lookup"><span data-stu-id="1c772-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="1c772-116">Haga clic en **Actualizar** después de establecer los filtros.</span><span class="sxs-lookup"><span data-stu-id="1c772-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="1c772-117">El gráfico de retención general muestra un resumen de la retención del usuario durante un período de tiempo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1c772-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="1c772-118">La cuadrícula muestra el número de usuarios retenidos según el generador de consultas en 2.</span><span class="sxs-lookup"><span data-stu-id="1c772-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="1c772-119">Cada fila representa una cohorte de usuarios que llevó a cabo cualquier evento en el periodo mostrado.</span><span class="sxs-lookup"><span data-stu-id="1c772-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="1c772-120">Cada celda de la fila muestra cuántos de esa cohorte regresaron al menos una vez en un periodo posterior.</span><span class="sxs-lookup"><span data-stu-id="1c772-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="1c772-121">Algunos usuarios pueden regresar en más de un periodo.</span><span class="sxs-lookup"><span data-stu-id="1c772-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="1c772-122">Las tarjetas de información muestran los cinco eventos de inicio más importantes y los cinco eventos devueltos principales para proporcionar a los usuarios una mejor comprensión de su informe de retención.</span><span class="sxs-lookup"><span data-stu-id="1c772-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Mantener el puntero sobre la retención](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="1c772-124">Los usuarios pueden mantener el puntero sobre las celdas de la herramienta Retención para acceder al botón de análisis y a la información que explica lo que significa cada celda.</span><span class="sxs-lookup"><span data-stu-id="1c772-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="1c772-125">El botón Análisis conduce al usuario a la herramienta Análisis con una consulta rellenada previamente para generar usuarios desde la celda.</span><span class="sxs-lookup"><span data-stu-id="1c772-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="1c772-126">Uso de eventos empresariales para realizar un seguimiento de la retención</span><span class="sxs-lookup"><span data-stu-id="1c772-126">Use business events to track retention</span></span>

<span data-ttu-id="1c772-127">Para obtener el análisis de retención más útil, mida los eventos que representan actividades empresariales importantes.</span><span class="sxs-lookup"><span data-stu-id="1c772-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="1c772-128">Por ejemplo, muchos usuarios podrían abrir una página de la aplicación sin jugar al juego que se muestra.</span><span class="sxs-lookup"><span data-stu-id="1c772-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="1c772-129">Al realizar solo el seguimiento de las vistas de página, se proporcionaría una estimación inexacta de cuántas personas vuelven a reproducir el juego después de haberlo jugado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1c772-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="1c772-130">Para obtener una visión clara de los jugadores que regresan, la aplicación debe enviar un evento personalizado cuando un usuario juega realmente.</span><span class="sxs-lookup"><span data-stu-id="1c772-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="1c772-131">Se recomienda codificar los eventos personalizados que representan las acciones clave del negocio y usarlos para realizar el análisis de retención.</span><span class="sxs-lookup"><span data-stu-id="1c772-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="1c772-132">Para obtener el resultado del juego, tiene que escribir una línea de código con el fin enviar un evento personalizado a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1c772-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="1c772-133">Si se escribe en el código de la página web o en Node.JS, se vería similar a esto:</span><span class="sxs-lookup"><span data-stu-id="1c772-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="1c772-134">O en el código del servidor ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="1c772-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="1c772-135">[Obtenga más información sobre la creación de eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="1c772-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1c772-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c772-136">Next steps</span></span>
- <span data-ttu-id="1c772-137">Para habilitar las experiencias de uso, empiece por enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [vistas de páginas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="1c772-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="1c772-138">Si ya ha enviado eventos personalizados o vistas de página, explore las herramientas de uso para obtener información sobre cómo los usuarios utilizan el servicio.</span><span class="sxs-lookup"><span data-stu-id="1c772-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="1c772-139">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="1c772-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="1c772-140">Embudos</span><span class="sxs-lookup"><span data-stu-id="1c772-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="1c772-141">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="1c772-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="1c772-142">Libros</span><span class="sxs-lookup"><span data-stu-id="1c772-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="1c772-143">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="1c772-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


