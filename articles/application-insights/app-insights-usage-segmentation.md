---
title: "Análisis de usuarios, sesiones y evento en Azure Application Insights | Microsoft Docs"
description: "Este artículo trata sobre el análisis de los usuarios de su aplicación web."
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="f4e08-103">Análisis de usuarios, sesiones y eventos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="f4e08-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="f4e08-104">Descubra cuándo los usuarios utilizan la aplicación web, en qué páginas que están más interesados, en qué ubicación se encuentran dichos usuarios, y los sistemas operativos y exploradores que emplean.</span><span class="sxs-lookup"><span data-stu-id="f4e08-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="f4e08-105">Analice la telemetría de uso y de negocio con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4e08-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="f4e08-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="f4e08-106">Get started</span></span>

<span data-ttu-id="f4e08-107">Si aún no ve los datos en las hojas de usuarios, sesiones o eventos de Application Insights, [obtenga información sobre cómo empezar a trabajar con las herramientas de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4e08-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="f4e08-108">La herramienta de segmentación de usuarios, sesiones y eventos</span><span class="sxs-lookup"><span data-stu-id="f4e08-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="f4e08-109">Tres de las hojas de uso usan la misma herramienta para segmentar y desglosar telemetría de su aplicación web desde tres perspectivas.</span><span class="sxs-lookup"><span data-stu-id="f4e08-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="f4e08-110">Mediante el filtrado y la división de los datos, puede descubrir información detallada sobre el uso relativo de distintas páginas y características.</span><span class="sxs-lookup"><span data-stu-id="f4e08-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="f4e08-111">**Herramienta de usuarios**: averigüe cuántas personas usan la aplicación y sus características.</span><span class="sxs-lookup"><span data-stu-id="f4e08-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="f4e08-112">Los usuarios se cuentan mediante el uso de identificadores anónimos almacenados en las cookies del explorador.</span><span class="sxs-lookup"><span data-stu-id="f4e08-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="f4e08-113">Una sola persona que usa distintos exploradores o máquinas se contarán como más de un usuario.</span><span class="sxs-lookup"><span data-stu-id="f4e08-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="f4e08-114">**Herramienta de sesiones**: la cantidad de sesiones de actividad de usuario que han incluido determinadas páginas y características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4e08-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="f4e08-115">Una sesión se cuenta después de media hora de inactividad del usuario, o después de 24 horas de uso continuas.</span><span class="sxs-lookup"><span data-stu-id="f4e08-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="f4e08-116">**Herramienta de eventos**: la frecuencia con la que se usan ciertas páginas y características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4e08-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="f4e08-117">Una vista de página se cuenta cuando un explorador carga una página de la aplicación, siempre que se haya [instrumentado](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="f4e08-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="f4e08-118">Un evento personalizado representa una repetición de algo que sucede en la aplicación, a menudo, una interacción del usuario como un clic en el botón o la realización de alguna tarea.</span><span class="sxs-lookup"><span data-stu-id="f4e08-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="f4e08-119">Inserte código en su aplicación para [generar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="f4e08-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Herramienta de uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="f4e08-121">Consulta de determinados usuarios</span><span class="sxs-lookup"><span data-stu-id="f4e08-121">Querying for Certain Users</span></span> 

<span data-ttu-id="f4e08-122">Explore distintos grupos de usuarios mediante ajustando las opciones de consulta en la parte superior de la herramienta Usuarios:</span><span class="sxs-lookup"><span data-stu-id="f4e08-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="f4e08-123">que usaron: elija eventos personalizados y vistas de página.</span><span class="sxs-lookup"><span data-stu-id="f4e08-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="f4e08-124">Durante: elija un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="f4e08-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="f4e08-125">Por: elija cómo se desglosarán los datos, por un periodo u otra propiedad como un explorador o una ciudad.</span><span class="sxs-lookup"><span data-stu-id="f4e08-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="f4e08-126">Dividir por: elija una propiedad por la que dividir o segmentar los datos.</span><span class="sxs-lookup"><span data-stu-id="f4e08-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="f4e08-127">Agregar filtros: limite la consulta a determinados usuarios, sesiones o eventos en función de sus propiedades, como un explorador o una ciudad.</span><span class="sxs-lookup"><span data-stu-id="f4e08-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="f4e08-128">Guardado e intercambio de informes</span><span class="sxs-lookup"><span data-stu-id="f4e08-128">Saving and sharing reports</span></span> 
<span data-ttu-id="f4e08-129">Puede guardar los informes de Usuarios, de forma privada (solo para usted) en la sección Mis informes, o bien con todos aquellos que tengan acceso a este recurso de Application Insights en la sección Informes compartidos.</span><span class="sxs-lookup"><span data-stu-id="f4e08-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="f4e08-130">Al guardar un informe o editar sus propiedades, elija "Intervalo de tiempo relativo actual" para guardar un informe con los datos continuamente actualizados, con lo que puede consultar el periodo que desee.</span><span class="sxs-lookup"><span data-stu-id="f4e08-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="f4e08-131">Elija "Intervalo de tiempo absoluto actual" para guardar un informe con un conjunto fijo de datos.</span><span class="sxs-lookup"><span data-stu-id="f4e08-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="f4e08-132">Tenga en cuenta que solo se almacenan datos de Application Insights durante 90 días, por lo que, si han pasado más de 90 días desde que guardó un informe con un intervalo de tiempo absoluto, el informe se mostrará vacío.</span><span class="sxs-lookup"><span data-stu-id="f4e08-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="f4e08-133">Instancias de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4e08-133">Example instances</span></span>

<span data-ttu-id="f4e08-134">La sección de instancias en el ejemplo muestra información sobre una serie de eventos, sesiones o usuarios que coinciden con la consulta actual.</span><span class="sxs-lookup"><span data-stu-id="f4e08-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="f4e08-135">Al tener en cuenta y explorar los comportamientos de los usuarios, además de los agregados, se puede proporcionar información sobre cómo se utiliza realmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4e08-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="f4e08-136">Información detallada</span><span class="sxs-lookup"><span data-stu-id="f4e08-136">Insights</span></span> 

<span data-ttu-id="f4e08-137">La barra lateral de Información detallada muestra grandes grupos los usuarios que comparten propiedades comunes.</span><span class="sxs-lookup"><span data-stu-id="f4e08-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="f4e08-138">Estos grupos pueden descubrir tendencias sorprendentes sobre cómo se usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4e08-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="f4e08-139">Por ejemplo, si el 40 % de todo el uso de la aplicación proviene de personas que usan una sola característica.</span><span class="sxs-lookup"><span data-stu-id="f4e08-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="f4e08-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4e08-140">Next steps</span></span>
- <span data-ttu-id="f4e08-141">Para habilitar las experiencias de uso, empiece por enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [vistas de páginas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="f4e08-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="f4e08-142">Si ya ha enviado eventos personalizados o vistas de página, explore las herramientas de uso para obtener información sobre cómo los usuarios utilizan el servicio.</span><span class="sxs-lookup"><span data-stu-id="f4e08-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="f4e08-143">Embudos</span><span class="sxs-lookup"><span data-stu-id="f4e08-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="f4e08-144">Retención</span><span class="sxs-lookup"><span data-stu-id="f4e08-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="f4e08-145">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="f4e08-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="f4e08-146">Libros</span><span class="sxs-lookup"><span data-stu-id="f4e08-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="f4e08-147">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="f4e08-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

