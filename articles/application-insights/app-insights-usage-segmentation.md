---
title: "análisis de aaaUser, sesiones y eventos en Azure Application Insights | Documentos de Microsoft"
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="81271-103">Análisis de usuarios, sesiones y eventos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="81271-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="81271-104">Descubra cuándo los usuarios utilizan la aplicación web, en qué páginas que están más interesados, en qué ubicación se encuentran dichos usuarios, y los sistemas operativos y exploradores que emplean.</span><span class="sxs-lookup"><span data-stu-id="81271-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="81271-105">Analice la telemetría de uso y de negocio con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81271-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="81271-106">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="81271-106">Get started</span></span>

<span data-ttu-id="81271-107">Si aún no ve los datos en los usuarios de hello, sesiones o las hojas de eventos en el portal de Application Insights hello, [Obtenga información acerca de cómo tooget a trabajar con herramientas de uso de hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81271-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="81271-108">herramienta de segmentación de los usuarios, sesiones y eventos Hola</span><span class="sxs-lookup"><span data-stu-id="81271-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="81271-109">Tres de usar hojas de uso de Hola Hola mismo telemetría herramienta de tooslice y dividir los datos desde la aplicación web desde tres perspectivas.</span><span class="sxs-lookup"><span data-stu-id="81271-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="81271-110">Mediante el filtrado y dividir los datos de hello, se puede descubrir información acerca del uso de relativa Hola de distintas páginas y características.</span><span class="sxs-lookup"><span data-stu-id="81271-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="81271-111">**Herramienta de usuarios**: averigüe cuántas personas usan la aplicación y sus características.</span><span class="sxs-lookup"><span data-stu-id="81271-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="81271-112">Los usuarios se cuentan mediante el uso de identificadores anónimos almacenados en las cookies del explorador.</span><span class="sxs-lookup"><span data-stu-id="81271-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="81271-113">Una sola persona que usa distintos exploradores o máquinas se contarán como más de un usuario.</span><span class="sxs-lookup"><span data-stu-id="81271-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="81271-114">**Herramienta de sesiones**: la cantidad de sesiones de actividad de usuario que han incluido determinadas páginas y características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81271-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="81271-115">Una sesión se cuenta después de media hora de inactividad del usuario, o después de 24 horas de uso continuas.</span><span class="sxs-lookup"><span data-stu-id="81271-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="81271-116">**Herramienta de eventos**: la frecuencia con la que se usan ciertas páginas y características de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81271-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="81271-117">Una vista de página se cuenta cuando un explorador carga una página de la aplicación, siempre que se haya [instrumentado](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="81271-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="81271-118">Un evento personalizado representa una ocurrencia de algo que sucede en la aplicación, a menudo una interacción del usuario como un botón, haga clic en u Hola realización de alguna tarea.</span><span class="sxs-lookup"><span data-stu-id="81271-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="81271-119">Inserte código en su aplicación demasiado[generar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="81271-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Herramienta de uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="81271-121">Consulta de determinados usuarios</span><span class="sxs-lookup"><span data-stu-id="81271-121">Querying for Certain Users</span></span> 

<span data-ttu-id="81271-122">Explorar distintos grupos de usuarios mediante el ajuste de opciones de consulta de hello en parte superior de Hola de herramienta de Hola a los usuarios:</span><span class="sxs-lookup"><span data-stu-id="81271-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="81271-123">que usaron: elija eventos personalizados y vistas de página.</span><span class="sxs-lookup"><span data-stu-id="81271-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="81271-124">Durante: elija un intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="81271-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="81271-125">Por: Elija cómo toobucket Hola datos, por un período de tiempo o por otra propiedad como explorador o una ciudad.</span><span class="sxs-lookup"><span data-stu-id="81271-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="81271-126">Dividir por: Elija una propiedad por los datos de hello toosplit o segmento.</span><span class="sxs-lookup"><span data-stu-id="81271-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="81271-127">Agregar filtros: Limitar Hola consultar toocertain a los usuarios, sesiones o eventos en función de sus propiedades, como el explorador o una ciudad.</span><span class="sxs-lookup"><span data-stu-id="81271-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="81271-128">Guardado e intercambio de informes</span><span class="sxs-lookup"><span data-stu-id="81271-128">Saving and sharing reports</span></span> 
<span data-ttu-id="81271-129">Puede guardar los informes de los usuarios, ya sea tooyou privada solo en la sección de Mis informes de hello, o comparten con todos los demás con toothis de acceso a recursos de Application Insights de hello sección informes compartidos.</span><span class="sxs-lookup"><span data-stu-id="81271-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="81271-130">Al guardar un informe o editar sus propiedades, elija toosave "Intervalo de tiempo relativa actual" un informe le continuamente actualiza datos, volviendo a un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="81271-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="81271-131">Elegir un informe con un conjunto fijo de datos de toosave "Intervalo de tiempo absoluto actual".</span><span class="sxs-lookup"><span data-stu-id="81271-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="81271-132">Tenga en cuenta que solo se almacenan datos de Application Insights durante 90 días, por lo que se guardó si han pasado más de 90 días desde un informe con un intervalo de tiempo absoluto, informe de Hola se mostrará vacío.</span><span class="sxs-lookup"><span data-stu-id="81271-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="81271-133">Instancias de ejemplo</span><span class="sxs-lookup"><span data-stu-id="81271-133">Example instances</span></span>

<span data-ttu-id="81271-134">Hola sección de instancias en el ejemplo muestra información sobre una serie de eventos que coinciden con la consulta actual de Hola, sesiones o usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="81271-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="81271-135">Teniendo en cuenta y explorar los comportamientos de Hola de individuos, en tooaggregates de suma, pueden proporcionar información sobre cómo se utiliza realmente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81271-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="81271-136">Información detallada</span><span class="sxs-lookup"><span data-stu-id="81271-136">Insights</span></span> 

<span data-ttu-id="81271-137">barra lateral de visión de Hello muestra grandes clústeres de los usuarios que comparten propiedades comunes.</span><span class="sxs-lookup"><span data-stu-id="81271-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="81271-138">Estos grupos pueden descubrir tendencias sorprendentes sobre cómo se usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81271-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="81271-139">Por ejemplo, si procede de 40% de todas las de uso de saludo de la aplicación de personas que usan una sola función.</span><span class="sxs-lookup"><span data-stu-id="81271-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="81271-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81271-140">Next steps</span></span>
- <span data-ttu-id="81271-141">uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="81271-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="81271-142">Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.</span><span class="sxs-lookup"><span data-stu-id="81271-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="81271-143">Embudos</span><span class="sxs-lookup"><span data-stu-id="81271-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="81271-144">Retención</span><span class="sxs-lookup"><span data-stu-id="81271-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="81271-145">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="81271-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="81271-146">Libros</span><span class="sxs-lookup"><span data-stu-id="81271-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="81271-147">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="81271-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

