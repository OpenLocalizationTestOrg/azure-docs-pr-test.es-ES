---
title: "Análisis de uso de aplicaciones web con Azure Application Insights | Microsoft Docs"
description: "Entender a los usuarios y lo qué hacen con su aplicación web."
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="e79c5-103">Análisis de uso de aplicaciones web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="e79c5-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="e79c5-104">¿Qué características de su aplicación web son más populares?</span><span class="sxs-lookup"><span data-stu-id="e79c5-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="e79c5-105">¿Los usuarios logran sus objetivos con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="e79c5-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="e79c5-106">¿Salen de ella en momentos concretos y vuelven más tarde?</span><span class="sxs-lookup"><span data-stu-id="e79c5-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="e79c5-107">[Azure Application Insights](app-insights-overview.md) lo ayudará a obtener información eficaz sobre cómo los usuarios usan su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e79c5-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="e79c5-108">Cada vez que actualice la aplicación, puede evaluar también si funciona bien para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e79c5-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="e79c5-109">Con este conocimiento, puede tomar decisiones basadas en datos sobre los ciclos de desarrollo siguientes.</span><span class="sxs-lookup"><span data-stu-id="e79c5-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="e79c5-110">Envío de telemetría desde la aplicación</span><span class="sxs-lookup"><span data-stu-id="e79c5-110">Send telemetry from your app</span></span>

<span data-ttu-id="e79c5-111">La mejor experiencia se obtiene mediante la instalación de Application Insights en el código de servidor de aplicaciones y en las páginas web.</span><span class="sxs-lookup"><span data-stu-id="e79c5-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="e79c5-112">Los componentes de cliente y servidor de la aplicación devuelven telemetría a Azure Portal para su análisis.</span><span class="sxs-lookup"><span data-stu-id="e79c5-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="e79c5-113">**Código de servidor:** instale el módulo adecuado para [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), u [otra aplicación ](app-insights-platforms.md).</span><span class="sxs-lookup"><span data-stu-id="e79c5-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="e79c5-114">*¿No desea instalar código del servidor? Simplemente [cree un recurso de Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="e79c5-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="e79c5-115">**Código de página web:** abra el [Azure Portal](https://portal.azure.com), abra el recurso de Application Insights para su aplicación y luego abra **Introducción > Supervisar y diagnosticar la aplicación del lado cliente**.</span><span class="sxs-lookup"><span data-stu-id="e79c5-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copie el script en el encabezado de la página web maestra.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="e79c5-117">**Obtener telemetría:** ejecute su proyecto en modo de depuración durante unos minutos y luego busque resultados en la hoja de información general en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e79c5-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="e79c5-118">Publique su aplicación para supervisar el rendimiento de su aplicación y descubra lo que hacen sus usuarios con ella.</span><span class="sxs-lookup"><span data-stu-id="e79c5-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="e79c5-119">Inclusión del identificador de usuario y de sesión en la telemetría</span><span class="sxs-lookup"><span data-stu-id="e79c5-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="e79c5-120">Para realizar un seguimiento de los usuarios a lo largo del tiempo, Application Insights necesita una manera de identificarlos.</span><span class="sxs-lookup"><span data-stu-id="e79c5-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="e79c5-121">La herramienta de eventos es la única herramienta de uso que no requiere un identificador de usuario o de sesión.</span><span class="sxs-lookup"><span data-stu-id="e79c5-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="e79c5-122">Empiece a enviar estos identificadores [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="e79c5-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="e79c5-123">Exploración de estadísticas y datos demográficos de uso</span><span class="sxs-lookup"><span data-stu-id="e79c5-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="e79c5-124">Descubra cuándo los usuarios utilizan la aplicación, en qué páginas que están más interesados, en qué ubicación se encuentran dichos usuarios, y los sistemas operativos y exploradores que emplean.</span><span class="sxs-lookup"><span data-stu-id="e79c5-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="e79c5-125">Los informes Usuarios y sesiones filtran los datos por páginas o eventos personalizados, y los segmentan por propiedades tales como la ubicación, el entorno y la página.</span><span class="sxs-lookup"><span data-stu-id="e79c5-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="e79c5-126">También puede agregar sus propios filtros.</span><span class="sxs-lookup"><span data-stu-id="e79c5-126">You can also add your own filters.</span></span>

![Usuarios](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="e79c5-128">La información de la derecha señala patrones de interés en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="e79c5-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="e79c5-129">El informe **Usuarios** indica el número de usuarios únicos que tienen acceso a las páginas dentro de los periodos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="e79c5-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="e79c5-130">(Los usuarios se cuentan mediante el uso de cookies.</span><span class="sxs-lookup"><span data-stu-id="e79c5-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="e79c5-131">Si alguien accede a su sitio con distintos exploradores o equipos cliente, o borra sus cookies, se contabilizarán de más de una vez.)</span><span class="sxs-lookup"><span data-stu-id="e79c5-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="e79c5-132">El informe **Sesiones** indica el número de sesiones de usuario que acceden al sitio.</span><span class="sxs-lookup"><span data-stu-id="e79c5-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="e79c5-133">Una sesión es un periodo de actividad por parte de un usuario, que finaliza con un periodo de inactividad de más de media hora.</span><span class="sxs-lookup"><span data-stu-id="e79c5-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="e79c5-134">Más información sobre las herramientas Usuarios, Sesiones y Eventos</span><span class="sxs-lookup"><span data-stu-id="e79c5-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="e79c5-135">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="e79c5-135">Page views</span></span>

<span data-ttu-id="e79c5-136">En la hoja Uso, haga clic en el icono de vistas de página para obtener un desglose de las páginas más populares:</span><span class="sxs-lookup"><span data-stu-id="e79c5-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![En la hoja de información general, haga clic en el gráfico de vistas de páginas.](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="e79c5-138">El ejemplo anterior es de un sitio web de juegos.</span><span class="sxs-lookup"><span data-stu-id="e79c5-138">The example above is from a games web site.</span></span> <span data-ttu-id="e79c5-139">A partir de los gráficos, podemos ver al instante:</span><span class="sxs-lookup"><span data-stu-id="e79c5-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="e79c5-140">El uso no ha mejorado durante la semana anterior.</span><span class="sxs-lookup"><span data-stu-id="e79c5-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="e79c5-141">¿Quizás debemos pensar en la optimización de motor de búsqueda?</span><span class="sxs-lookup"><span data-stu-id="e79c5-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="e79c5-142">Tennis es la página de juegos más popular.</span><span class="sxs-lookup"><span data-stu-id="e79c5-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="e79c5-143">Vamos a centrarnos en mejorar aún más esta página.</span><span class="sxs-lookup"><span data-stu-id="e79c5-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="e79c5-144">Por término medio, los usuarios visitan la página Tennis una tres veces por semana.</span><span class="sxs-lookup"><span data-stu-id="e79c5-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="e79c5-145">(Hay unas tres veces más sesiones que usuarios.)</span><span class="sxs-lookup"><span data-stu-id="e79c5-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="e79c5-146">La mayoría de usuarios visitan el sitio durante la semana laboral en EE. UU. y en el horario laborable.</span><span class="sxs-lookup"><span data-stu-id="e79c5-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="e79c5-147">Quizás deberíamos proporcionar un botón "ocultar rápidamente" en la página web.</span><span class="sxs-lookup"><span data-stu-id="e79c5-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="e79c5-148">Las [anotaciones](app-insights-annotations.md) en el gráfico muestran cuándo se implementaron nuevas versiones del sitio web.</span><span class="sxs-lookup"><span data-stu-id="e79c5-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="e79c5-149">Ninguna de las implementaciones ha tenido un efecto notable sobre el uso.</span><span class="sxs-lookup"><span data-stu-id="e79c5-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="e79c5-150">¿Qué ocurre si desea investigar el tráfico de su sitio con más detalle, por ejemplo, dividiendo por propiedad personalizada que el sitio envía en su telemetría de vista de página?</span><span class="sxs-lookup"><span data-stu-id="e79c5-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="e79c5-151">Abra la herramienta **Eventos** del menú de recursos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e79c5-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="e79c5-152">Esta herramienta permite analizar el número de eventos personalizados y vistas de página que se enviaron desde su aplicación, en función de una variedad de opciones de filtrado, cohorte y segmentación.</span><span class="sxs-lookup"><span data-stu-id="e79c5-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="e79c5-153">En la lista desplegable "que usaron", seleccione "Cualquier página de vista".</span><span class="sxs-lookup"><span data-stu-id="e79c5-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="e79c5-154">En la lista desplegable de "Dividir por", seleccione una propiedad por la que va a dividir la telemetría de vista de página.</span><span class="sxs-lookup"><span data-stu-id="e79c5-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="e79c5-155">Retención : ¿cuántos usuarios regresan?</span><span class="sxs-lookup"><span data-stu-id="e79c5-155">Retention - how many users come back?</span></span>

<span data-ttu-id="e79c5-156">Retención lo ayudará a comprender la frecuencia con la que los usuarios vuelven a usar su aplicación, en función de las cohortes de usuarios que realizan alguna acción empresarial durante un intervalo de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="e79c5-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="e79c5-157">Qué características específicas provocan que los usuarios vuelvan más veces que otras</span><span class="sxs-lookup"><span data-stu-id="e79c5-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="e79c5-158">Formular hipótesis basadas en datos de usuarios reales</span><span class="sxs-lookup"><span data-stu-id="e79c5-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="e79c5-159">Determinar si la retención es un problema del producto</span><span class="sxs-lookup"><span data-stu-id="e79c5-159">Determine whether retention is a problem in your product</span></span> 

![Retención](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="e79c5-161">Los controles de retención de la parte superior permiten definir eventos específicos y el intervalo de tiempo para calcular la retención.</span><span class="sxs-lookup"><span data-stu-id="e79c5-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="e79c5-162">El gráfico situado en la parte central proporciona una representación visual del porcentaje total de retención por el intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="e79c5-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="e79c5-163">El gráfico de la parte inferior representa la retención individual en un periodo determinado.</span><span class="sxs-lookup"><span data-stu-id="e79c5-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="e79c5-164">Este nivel de detalle permite entender lo que hacen los usuarios y qué podría afectar al regreso de los usuarios con una granularidad más detallada.</span><span class="sxs-lookup"><span data-stu-id="e79c5-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="e79c5-165">Más información de la herramienta Retención</span><span class="sxs-lookup"><span data-stu-id="e79c5-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="e79c5-166">Eventos de negocio personalizados</span><span class="sxs-lookup"><span data-stu-id="e79c5-166">Custom business events</span></span>

<span data-ttu-id="e79c5-167">Para obtener una idea clara de lo que los usuarios hacen con la aplicación web, es útil insertar líneas de código para registrar eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="e79c5-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="e79c5-168">Estos eventos pueden realizar un seguimiento desde acciones del usuario detalladas como hacer clic en botones específicos hasta eventos de negocio más importantes como realizar una compra o ganar una partida.</span><span class="sxs-lookup"><span data-stu-id="e79c5-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="e79c5-169">Aunque, en algunos casos, las vistas de página pueden representar eventos útiles, en general, no es así.</span><span class="sxs-lookup"><span data-stu-id="e79c5-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="e79c5-170">Un usuario puede abrir una página de un producto sin necesidad de adquirirlo.</span><span class="sxs-lookup"><span data-stu-id="e79c5-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="e79c5-171">Con los eventos específicos del negocio, puede realizar un gráfico del progreso de los usuarios en su sitio.</span><span class="sxs-lookup"><span data-stu-id="e79c5-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="e79c5-172">Puede averiguar sus preferencias para diferentes opciones y en qué partes salen o tienen dificultades.</span><span class="sxs-lookup"><span data-stu-id="e79c5-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="e79c5-173">Con este conocimiento, puedan tomar decisiones fundamentadas en lo que respecta a las prioridades del trabajo pendiente en materia de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e79c5-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="e79c5-174">Los eventos se pueden registrar en la página web:</span><span class="sxs-lookup"><span data-stu-id="e79c5-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="e79c5-175">O bien, en el lado del servidor de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="e79c5-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="e79c5-176">Puede adjuntar los valores de propiedad a estos eventos, para que pueda filtrar o dividir los eventos al examinarlos en el portal.</span><span class="sxs-lookup"><span data-stu-id="e79c5-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="e79c5-177">Además, se adjunta un conjunto estándar de propiedades a cada evento, como el identificador de usuario anónimo, lo que permite realizar un seguimiento de la secuencia de actividades de un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="e79c5-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="e79c5-178">Obtenga más información sobre los [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) y las [propiedades](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="e79c5-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="e79c5-179">Eventos de segmentación y desglose</span><span class="sxs-lookup"><span data-stu-id="e79c5-179">Slice and dice events</span></span>

<span data-ttu-id="e79c5-180">En las herramientas Usuarios, Sesiones y Eventos, puede segmentar y desglosar los eventos personalizados por usuario, nombre del evento y propiedades.</span><span class="sxs-lookup"><span data-stu-id="e79c5-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="e79c5-181">![Usuarios](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="e79c5-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="e79c5-182">Diseño de la telemetría con la aplicación</span><span class="sxs-lookup"><span data-stu-id="e79c5-182">Design the telemetry with the app</span></span>

<span data-ttu-id="e79c5-183">Al diseñar cada característica de la aplicación, tenga en cuenta cómo va a medir su éxito con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e79c5-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="e79c5-184">Decida qué eventos empresariales necesita registrar y codifique las llamadas de seguimiento de esos eventos en la aplicación desde el principio.</span><span class="sxs-lookup"><span data-stu-id="e79c5-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="e79c5-185">Prueba A | B</span><span class="sxs-lookup"><span data-stu-id="e79c5-185">A | B Testing</span></span>
<span data-ttu-id="e79c5-186">Si no conoce qué variante de una característica tendrá más éxito, publique ambas para que estén accesibles a los diferentes usuarios.</span><span class="sxs-lookup"><span data-stu-id="e79c5-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="e79c5-187">Mida el éxito de cada una y, a continuación, cambie a una versión unificada.</span><span class="sxs-lookup"><span data-stu-id="e79c5-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="e79c5-188">Para realizar esta técnica, adjunte valores de propiedad distintas a toda la telemetría que se envía con cada versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e79c5-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="e79c5-189">Puede hacerlo al definir las propiedades en el TelemetryContext activo.</span><span class="sxs-lookup"><span data-stu-id="e79c5-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="e79c5-190">Estas propiedades predeterminadas se agregan a cada mensaje de telemetría que envía la aplicación: no solo los mensajes personalizados, sino también la telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="e79c5-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="e79c5-191">En el portal de Application Insights, podrá filtrar y dividir los datos en los valores de propiedad, con el fin de comparar las distintas versiones.</span><span class="sxs-lookup"><span data-stu-id="e79c5-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="e79c5-192">Para ello, [configure un inicializador de telemetría](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="e79c5-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="e79c5-193">En el inicializador de la aplicación web, como Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="e79c5-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="e79c5-194">Todos los nuevos clientes de telemetría agregan automáticamente el valor de propiedad especificado.</span><span class="sxs-lookup"><span data-stu-id="e79c5-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="e79c5-195">La telemetría individual puede invalidar los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="e79c5-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e79c5-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e79c5-196">Next steps</span></span>
   - [<span data-ttu-id="e79c5-197">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="e79c5-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="e79c5-198">Embudos</span><span class="sxs-lookup"><span data-stu-id="e79c5-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="e79c5-199">Retención</span><span class="sxs-lookup"><span data-stu-id="e79c5-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="e79c5-200">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="e79c5-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="e79c5-201">Libros</span><span class="sxs-lookup"><span data-stu-id="e79c5-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="e79c5-202">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="e79c5-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
