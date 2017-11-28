---
title: "análisis de aaaUsage para aplicaciones web con Azure Application Insights | Documentos de Microsoft"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="75c61-103">Análisis de uso de aplicaciones web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="75c61-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="75c61-104">¿Qué características de su aplicación web son más populares?</span><span class="sxs-lookup"><span data-stu-id="75c61-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="75c61-105">¿Los usuarios logran sus objetivos con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="75c61-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="75c61-106">¿Salen de ella en momentos concretos y vuelven más tarde?</span><span class="sxs-lookup"><span data-stu-id="75c61-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="75c61-107">[Azure Application Insights](app-insights-overview.md) lo ayudará a obtener información eficaz sobre cómo los usuarios usan su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="75c61-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="75c61-108">Cada vez que actualice la aplicación, puede evaluar también si funciona bien para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="75c61-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="75c61-109">Con este conocimiento, puede tomar decisiones basadas en datos sobre los ciclos de desarrollo siguientes.</span><span class="sxs-lookup"><span data-stu-id="75c61-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="75c61-110">Envío de telemetría desde la aplicación</span><span class="sxs-lookup"><span data-stu-id="75c61-110">Send telemetry from your app</span></span>

<span data-ttu-id="75c61-111">mejor experiencia de Hola se obtiene mediante la instalación de Application Insights en el código de servidor de la aplicación y en las páginas web.</span><span class="sxs-lookup"><span data-stu-id="75c61-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="75c61-112">componentes de cliente y servidor de saludo de la aplicación envían telemetría atrás toohello portal de Azure para su análisis.</span><span class="sxs-lookup"><span data-stu-id="75c61-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="75c61-113">**Código de servidor:** módulo apropiado de Hola de instalación para su [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), o [otros](app-insights-platforms.md) aplicación.</span><span class="sxs-lookup"><span data-stu-id="75c61-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="75c61-114">*¿No desea que el código del servidor de tooinstall? Simplemente [cree un recurso de Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="75c61-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="75c61-115">**Código de la página Web:** Hola abierto [portal de Azure](https://portal.azure.com), abra el recurso de Application Insights de hello para la aplicación y, a continuación, abra **Introducción > supervisar y diagnosticar cliente**.</span><span class="sxs-lookup"><span data-stu-id="75c61-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copie el script de Hola en encabezado de hello de la página web principal.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="75c61-117">**Obtener telemetría:** ejecutar el proyecto en modo de depuración durante unos minutos y, a continuación, compruebe los resultados en la hoja de información general de hello en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="75c61-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="75c61-118">Publique su aplicación toomonitor el rendimiento de la aplicación y averiguar lo que hacen los usuarios con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="75c61-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="75c61-119">Inclusión del identificador de usuario y de sesión en la telemetría</span><span class="sxs-lookup"><span data-stu-id="75c61-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="75c61-120">tootrack a los usuarios con el tiempo, Application Insights requiere un tooidentify manera ellos.</span><span class="sxs-lookup"><span data-stu-id="75c61-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="75c61-121">herramienta eventos Hola Hola única herramienta de uso que no requiere un identificador de usuario o un identificador de sesión.</span><span class="sxs-lookup"><span data-stu-id="75c61-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="75c61-122">Empiece a enviar estos identificadores [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="75c61-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="75c61-123">Exploración de estadísticas y datos demográficos de uso</span><span class="sxs-lookup"><span data-stu-id="75c61-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="75c61-124">Descubra cuándo los usuarios utilizan la aplicación, en qué páginas que están más interesados, en qué ubicación se encuentran dichos usuarios, y los sistemas operativos y exploradores que emplean.</span><span class="sxs-lookup"><span data-stu-id="75c61-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="75c61-125">informes de usuarios y sesiones de Hello filtrar los datos por páginas o eventos personalizados y segmentación por propiedades tales como la ubicación, el entorno y la página.</span><span class="sxs-lookup"><span data-stu-id="75c61-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="75c61-126">También puede agregar sus propios filtros.</span><span class="sxs-lookup"><span data-stu-id="75c61-126">You can also add your own filters.</span></span>

![Usuarios](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="75c61-128">Visión en hello derecho señalar patrones de interés en el conjunto de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="75c61-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="75c61-129">Hola **usuarios** informe cuenta los números de Hola de usuarios únicos que tienen acceso a las páginas dentro de los períodos de tiempo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="75c61-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="75c61-130">(Los usuarios se cuentan mediante el uso de cookies.</span><span class="sxs-lookup"><span data-stu-id="75c61-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="75c61-131">Si alguien accede a su sitio con distintos exploradores o equipos cliente, o borra sus cookies, se contabilizarán de más de una vez.)</span><span class="sxs-lookup"><span data-stu-id="75c61-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="75c61-132">Hola **sesiones** informe cuenta el número de Hola de sesiones de usuario que tienen acceso al sitio.</span><span class="sxs-lookup"><span data-stu-id="75c61-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="75c61-133">Una sesión es un periodo de actividad por parte de un usuario, que finaliza con un periodo de inactividad de más de media hora.</span><span class="sxs-lookup"><span data-stu-id="75c61-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="75c61-134">Más información acerca de las herramientas de los usuarios, sesiones y los eventos de Hola</span><span class="sxs-lookup"><span data-stu-id="75c61-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="75c61-135">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="75c61-135">Page views</span></span>

<span data-ttu-id="75c61-136">Desde la hoja de uso de hello, click-through Hola vistas de página icono tooget un desglose de las páginas más populares:</span><span class="sxs-lookup"><span data-stu-id="75c61-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Desde la hoja de información general de hello, haga clic en hello gráfico de vistas de página](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="75c61-138">ejemplo de Hola anterior es de un sitio web de juegos.</span><span class="sxs-lookup"><span data-stu-id="75c61-138">hello example above is from a games web site.</span></span> <span data-ttu-id="75c61-139">De los gráficos de hello, podemos ver al instante:</span><span class="sxs-lookup"><span data-stu-id="75c61-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="75c61-140">Uso no se ha mejorado en hello semana pasada.</span><span class="sxs-lookup"><span data-stu-id="75c61-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="75c61-141">¿Quizás debemos pensar en la optimización de motor de búsqueda?</span><span class="sxs-lookup"><span data-stu-id="75c61-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="75c61-142">Tenis es la página de juego más popular de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="75c61-143">Este artículo nos centraremos en la página toothis de mejoras aún más.</span><span class="sxs-lookup"><span data-stu-id="75c61-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="75c61-144">En promedio, los usuarios visitar página de tenis de hello aproximadamente tres veces por semana.</span><span class="sxs-lookup"><span data-stu-id="75c61-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="75c61-145">(Hay unas tres veces más sesiones que usuarios.)</span><span class="sxs-lookup"><span data-stu-id="75c61-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="75c61-146">La mayoría de los usuarios visitan el sitio de Hola durante la semana laboral de hello Estados Unidos y en horario laboral.</span><span class="sxs-lookup"><span data-stu-id="75c61-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="75c61-147">Quizás que deberíamos proporcionarle un botón "Ocultar rápido" en la página web de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="75c61-148">Hola [anotaciones](app-insights-annotations.md) en el gráfico de hello aparecerán cuando se implementaron las nuevas versiones del sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="75c61-149">Ninguna de las implementaciones de hello recientes tenía un efecto notable en uso.</span><span class="sxs-lookup"><span data-stu-id="75c61-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="75c61-150">¿Qué ocurre si desea sitio de tooyour tooinvestigate Hola tráfico con más detalle, como la división de una propiedad personalizada, que el sitio envía en su telemetría de vista de página?</span><span class="sxs-lookup"><span data-stu-id="75c61-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="75c61-151">Abra hello **eventos** herramienta en el menú de recursos de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="75c61-152">Esta herramienta permite analizar el número de eventos personalizados y vistas de página que se enviaron desde su aplicación, en función de una variedad de opciones de filtrado, cohorte y segmentación.</span><span class="sxs-lookup"><span data-stu-id="75c61-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="75c61-153">En la lista desplegable "Que usa" Hola, seleccione "Vista de página Any".</span><span class="sxs-lookup"><span data-stu-id="75c61-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="75c61-154">En la lista desplegable de "División por" Hola, seleccione una propiedad por qué toosplit la página Ver telemetría.</span><span class="sxs-lookup"><span data-stu-id="75c61-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="75c61-155">Retención : ¿cuántos usuarios regresan?</span><span class="sxs-lookup"><span data-stu-id="75c61-155">Retention - how many users come back?</span></span>

<span data-ttu-id="75c61-156">Retención le ayudará a comprender la frecuencia con los usuarios devuelven toouse su aplicación, en función de las cohortes de usuarios que realizan alguna acción empresarial durante un depósito de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="75c61-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="75c61-157">Comprender qué características específicas hacer que los usuarios toocome back más que otras personas</span><span class="sxs-lookup"><span data-stu-id="75c61-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="75c61-158">Formular hipótesis basadas en datos de usuarios reales</span><span class="sxs-lookup"><span data-stu-id="75c61-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="75c61-159">Determinar si la retención es un problema del producto</span><span class="sxs-lookup"><span data-stu-id="75c61-159">Determine whether retention is a problem in your product</span></span> 

![Retención](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="75c61-161">los controles de retención de Hello en la parte superior permiten toodefine eventos específicos y la conservación de toocalculate de intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="75c61-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="75c61-162">gráfico situado en medio de Hola Hola proporciona una representación visual de hello porcentaje total de retención por hello intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="75c61-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="75c61-163">gráfico de Hello en la parte inferior de hello representa retención individual en un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="75c61-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="75c61-164">Este nivel de detalle permite toounderstand hacen qué los usuarios y qué pueden afectar a devolver a los usuarios con una granularidad más detallada.</span><span class="sxs-lookup"><span data-stu-id="75c61-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="75c61-165">Más información acerca de la herramienta de retención de Hola</span><span class="sxs-lookup"><span data-stu-id="75c61-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="75c61-166">Eventos de negocio personalizados</span><span class="sxs-lookup"><span data-stu-id="75c61-166">Custom business events</span></span>

<span data-ttu-id="75c61-167">tooget una idea clara de lo que los usuarios hacer con la aplicación web, resulta útil tooinsert líneas de eventos personalizados de código toolog.</span><span class="sxs-lookup"><span data-stu-id="75c61-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="75c61-168">Estos eventos pueden realizar un seguimiento de nada de las acciones del usuario detallada como hacer clic en botones específicos, toomore los eventos significativos para el negocio, como realizar una compra o ganar una partida.</span><span class="sxs-lookup"><span data-stu-id="75c61-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="75c61-169">Aunque, en algunos casos, las vistas de página pueden representar eventos útiles, en general, no es así.</span><span class="sxs-lookup"><span data-stu-id="75c61-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="75c61-170">Un usuario puede abrir una página del producto sin necesidad de adquirir el producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="75c61-171">Con los eventos específicos del negocio, puede realizar un gráfico del progreso de los usuarios en su sitio.</span><span class="sxs-lookup"><span data-stu-id="75c61-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="75c61-172">Puede averiguar sus preferencias para diferentes opciones y en qué partes salen o tienen dificultades.</span><span class="sxs-lookup"><span data-stu-id="75c61-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="75c61-173">Con este conocimiento, puedan tomar decisiones fundamentadas sobre prioridades de hello en el trabajo pendiente de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="75c61-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="75c61-174">Eventos se pueden registrar en la página web de hello:</span><span class="sxs-lookup"><span data-stu-id="75c61-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="75c61-175">O en el lado del servidor hello de aplicación web de hello:</span><span class="sxs-lookup"><span data-stu-id="75c61-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="75c61-176">Puede asociar eventos de toothese de valores de propiedad, de forma que puede filtrar o dividir los eventos de hello al examinar en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="75c61-177">Además, un conjunto estándar de propiedades es evento tooeach adjunta, como Id. de usuario anónimo, lo que permite la secuencia de hello tootrace de actividades de un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="75c61-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="75c61-178">Obtenga más información sobre los [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) y las [propiedades](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="75c61-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="75c61-179">Eventos de segmentación y desglose</span><span class="sxs-lookup"><span data-stu-id="75c61-179">Slice and dice events</span></span>

<span data-ttu-id="75c61-180">En herramientas de los usuarios, sesiones y los eventos de hello, puede segmentar y reorganizar los eventos personalizados por usuario, nombre del evento y propiedades.</span><span class="sxs-lookup"><span data-stu-id="75c61-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="75c61-181">![Usuarios](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="75c61-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="75c61-182">Diseño Hola telemetría con la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="75c61-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="75c61-183">Al diseñar cada característica de la aplicación, tenga en cuenta cómo va toomeasure su éxito con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="75c61-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="75c61-184">Decidir qué eventos de negocios que necesita toorecord y el código Hola llamadas para los eventos de seguimiento en la aplicación de Hola se inicia.</span><span class="sxs-lookup"><span data-stu-id="75c61-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="75c61-185">Prueba A | B</span><span class="sxs-lookup"><span data-stu-id="75c61-185">A | B Testing</span></span>
<span data-ttu-id="75c61-186">Si no sabe qué variante de una característica tendrá más éxito, liberar ambos, hacer que los usuarios toodifferent accesible.</span><span class="sxs-lookup"><span data-stu-id="75c61-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="75c61-187">Medir el éxito de Hola de cada uno y, a continuación, mover tooa unificada versión.</span><span class="sxs-lookup"><span data-stu-id="75c61-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="75c61-188">Para que esta técnica, debe adjuntar telemetría Hola de tooall de valores de propiedad distintiva que se envía con cada versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="75c61-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="75c61-189">Puede hacerlo mediante la definición de propiedades en hello TelemetryContext active.</span><span class="sxs-lookup"><span data-stu-id="75c61-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="75c61-190">Estas propiedades predeterminadas se agregan envía el mensaje de telemetría tooevery que Hola aplicación - no solo los mensajes personalizados, pero también telemetría estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="75c61-191">En el portal de Application Insights hello, filtrar y dividir los datos en los valores de propiedad hello, así como versiones diferentes de toocompare Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="75c61-192">toodo, [configurar un inicializador de telemetría](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="75c61-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="75c61-193">En el inicializador de aplicación de hello web como Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="75c61-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="75c61-194">TelemetryClients nuevo todos los agrega automáticamente el valor de propiedad de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="75c61-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="75c61-195">Eventos de telemetría individual pueden invalidar los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="75c61-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75c61-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75c61-196">Next steps</span></span>
   - [<span data-ttu-id="75c61-197">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="75c61-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="75c61-198">Embudos</span><span class="sxs-lookup"><span data-stu-id="75c61-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="75c61-199">Retención</span><span class="sxs-lookup"><span data-stu-id="75c61-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="75c61-200">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="75c61-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="75c61-201">Libros</span><span class="sxs-lookup"><span data-stu-id="75c61-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="75c61-202">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="75c61-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
