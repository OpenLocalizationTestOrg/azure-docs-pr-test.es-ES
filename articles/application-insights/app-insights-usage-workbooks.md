---
title: aaaInvestigate y recurso compartido de datos de uso con libros interactivos en Azure Application Insights | Documentos de Microsoft
description: "Este artículo trata sobre el análisis de los usuarios de su aplicación web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="b3615-103">Investigación y uso compartido de datos de uso con libros interactivos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b3615-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="b3615-104">Los libros combinan las visualizaciones de datos de [Azure Application Insights](app-insights-overview.md), las [consultas de Analytics](app-insights-analytics.md) y texto en documentos interactivos.</span><span class="sxs-lookup"><span data-stu-id="b3615-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="b3615-105">Los libros son puede ser editados por otros miembros del equipo con acceso toohello mismo recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3615-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="b3615-106">Esto significa hello las consultas y los controles utilizado toocreate un libro son tooother disponibles cuando los usuarios visiten libro hello, haciéndolos tooexplore fácil, ampliar y buscar errores.</span><span class="sxs-lookup"><span data-stu-id="b3615-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="b3615-107">Los libros son útiles en escenarios como:</span><span class="sxs-lookup"><span data-stu-id="b3615-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="b3615-108">Explorar el uso de saludo de la aplicación si no conoce de antemano las métricas de Hola de interés: número de usuarios, tasas de retención, las tasas de conversión, etcetera. A diferencia de otras herramientas de análisis de uso de Application Insights, los libros le permiten combinar varios tipos de visualizaciones y análisis, lo cual los hace idóneos para este tipo de exploración de forma libre.</span><span class="sxs-lookup"><span data-stu-id="b3615-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="b3615-109">Explicar equipo tooyour el rendimiento de una característica recientemente publicada, por el usuario que muestra los recuentos de interacciones de claves y otras métricas.</span><span class="sxs-lookup"><span data-stu-id="b3615-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="b3615-110">Uso compartido de resultados de Hola de una A / B experimentar en su aplicación con otros miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="b3615-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="b3615-111">Puede explicar objetivos de Hola para hello experimentar con texto, a continuación muestran cada métrica de uso y consulta de análisis usa experimento de hello tooevaluate, junto con la espera de llamada clara de si cada métrica era por encima o por debajo-las destino.</span><span class="sxs-lookup"><span data-stu-id="b3615-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="b3615-112">Impacto de Hola de una interrupción de informes sobre el uso de saludo de la aplicación, la combinación de datos, texto de explicación y una explicación de las interrupciones de tooprevent pasos siguientes Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="b3615-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="b3615-113">El recurso de Application Insights debe contener las vistas de página o los libros de toouse de eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="b3615-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="b3615-114">[Obtenga información acerca de cómo tooset la página de aplicación toocollect vistas automáticamente con hello Application Insights JavaScript SDK](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="b3615-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="b3615-115">Edición, reorganización, clonación y eliminación de secciones de libro</span><span class="sxs-lookup"><span data-stu-id="b3615-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="b3615-116">Un libro está compuesto de secciones: visualizaciones de uso que se pueden editar independientemente, gráficos, tablas, texto o resultados de consultas de Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3615-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="b3615-117">contenido de hello tooedit de una sección del libro, haga clic en hello **editar** botón siguiente y toohello derecha de la sección del libro de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3615-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Controles de edición de secciones de libros de Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="b3615-119">Cuando haya terminado editar una sección, haga clic en **realiza edición** en esquina Hola inferior izquierda de la sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3615-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="b3615-120">toocreate un duplicado de una sección, haga clic en hello **clonar esta sección** icono.</span><span class="sxs-lookup"><span data-stu-id="b3615-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="b3615-121">Crear secciones duplicadas es un tooiterate tooway excelente en una consulta sin perder las iteraciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="b3615-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="b3615-122">toomove hacia arriba una sección en un libro, haga clic en hello **se desplazan hacia arriba** o **Bajar** icono.</span><span class="sxs-lookup"><span data-stu-id="b3615-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="b3615-123">tooremove una sección de forma permanente, haga clic en hello **quitar** icono.</span><span class="sxs-lookup"><span data-stu-id="b3615-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="b3615-124">Incorporación de secciones de visualización de datos de uso</span><span class="sxs-lookup"><span data-stu-id="b3615-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="b3615-125">Los libros ofrecen cuatro tipos de visualizaciones de análisis de uso integradas.</span><span class="sxs-lookup"><span data-stu-id="b3615-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="b3615-126">Cada uno de ellos responde a una pregunta común acerca del uso de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3615-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="b3615-127">tooadd tablas y gráficos que no sea de estos cuatro secciones, agregue secciones de consultas de análisis (ver abajo).</span><span class="sxs-lookup"><span data-stu-id="b3615-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="b3615-128">tooadd a los usuarios, sesiones, eventos o retención sección tooyour libro, use hello **agregar usuarios** o en otro botón correspondiente en parte inferior de Hola de libro de Hola o en parte inferior de Hola de cualquier sección.</span><span class="sxs-lookup"><span data-stu-id="b3615-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![Sección Usuarios en los libros](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="b3615-130">Las secciones **Usuarios** dan respuesta a la pregunta "¿cuántos usuarios vieron una página determinada o utilizaron alguna característica de mi sitio?"</span><span class="sxs-lookup"><span data-stu-id="b3615-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="b3615-131">Las secciones **Sesiones** dan respuesta a la pregunta "¿cuántas sesiones emplearon los usuarios para ver una página determinada o usar alguna característica de mi sitio?"</span><span class="sxs-lookup"><span data-stu-id="b3615-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="b3615-132">Las secciones **Eventos** dan respuesta a la pregunta "¿cuántas veces vieron los usuarios una página determinada o utilizaron alguna característica de mi sitio?"</span><span class="sxs-lookup"><span data-stu-id="b3615-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="b3615-133">Cada uno de estos tipos de tres sección ofrece Hola mismos conjuntos de controles y visualizaciones:</span><span class="sxs-lookup"><span data-stu-id="b3615-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="b3615-134">Más información sobre la edición de las secciones Usuarios, Sesiones y Eventos</span><span class="sxs-lookup"><span data-stu-id="b3615-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="b3615-135">Alternar gráfico principal de hello, cuadrículas de histograma, visión automática y visualizaciones de los usuarios de ejemplo con hello **Mostrar gráfico**, **Mostrar cuadrícula**, **mostrar visión**y **Ejemplo de estos usuarios** casillas de verificación en la parte superior de Hola de cada sección.</span><span class="sxs-lookup"><span data-stu-id="b3615-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![Sección Retención en los libros](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="b3615-137">Las secciones **Retención** dan respuesta a la pregunta: "De las personas que vieron una página determinada o usaron alguna característica en un día o semana concretos, ¿cuántos regresaron otro día o semana posteriores?"</span><span class="sxs-lookup"><span data-stu-id="b3615-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="b3615-138">Más información acerca de la edición de las secciones de retención</span><span class="sxs-lookup"><span data-stu-id="b3615-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="b3615-139">Alternar Hola opcionales retención total del gráfico mediante hello **Mostrar gráfico de retención global** casilla situada en la parte superior de Hola de sección Hola.</span><span class="sxs-lookup"><span data-stu-id="b3615-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="b3615-140">Incorporación de secciones de análisis de Application Insights</span><span class="sxs-lookup"><span data-stu-id="b3615-140">Adding Application Insights Analytics sections</span></span>

![Sección de análisis en los libros](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="b3615-142">tooadd un libro de tooyour sección de consulta de análisis de visión de aplicaciones, usar hello **consulta de análisis de agregar** botón final Hola de libro de hello, o en parte inferior de Hola de cualquier sección.</span><span class="sxs-lookup"><span data-stu-id="b3615-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="b3615-143">Las secciones de consulta de análisis le permiten agregar consultas arbitrarias sobre los datos de Application Insights a los libros.</span><span class="sxs-lookup"><span data-stu-id="b3615-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="b3615-144">Esta flexibilidad significa que las secciones de consultas de análisis deben ser su go-toofor responder a preguntas sobre el sitio que no sea de hello cuatro mencionado anteriormente para los usuarios, sesiones, eventos y retención, como:</span><span class="sxs-lookup"><span data-stu-id="b3615-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="b3615-145">¿Cuántas excepciones hizo su throw sitio durante Hola mismo período como un descenso en cuanto al uso de tiempo?</span><span class="sxs-lookup"><span data-stu-id="b3615-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="b3615-146">¿Cuál era la distribución de Hola de tiempos de carga de página para los usuarios que vean algunos página?</span><span class="sxs-lookup"><span data-stu-id="b3615-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="b3615-147">¿Cuántos usuarios vieron un conjunto de páginas determinado de su sitio, pero no otro?</span><span class="sxs-lookup"><span data-stu-id="b3615-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="b3615-148">Esto puede resultar útil toounderstand si tiene clústeres de los usuarios que utilizan distintos subconjuntos de funcionalidad de su sitio (usar hello `join` operador con hello `kind=leftanti` modificador Hola lenguaje de consultas de análisis de registros).</span><span class="sxs-lookup"><span data-stu-id="b3615-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="b3615-149">Hola de uso [referencia del lenguaje de consulta de análisis de registro](https://docs.loganalytics.io/) toolearn más acerca de cómo escribir consultas.</span><span class="sxs-lookup"><span data-stu-id="b3615-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="b3615-150">Adición de texto y secciones de Markdown</span><span class="sxs-lookup"><span data-stu-id="b3615-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="b3615-151">Agregar títulos, explicaciones y libros de comentarios tooyour le ayuda a convertir un conjunto de tablas y gráficos en una descripción.</span><span class="sxs-lookup"><span data-stu-id="b3615-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="b3615-152">Las secciones de texto en los libros admiten hello [sintaxis de Markdown](https://daringfireball.net/projects/markdown/) de formato de texto, como encabezados, negrita, cursiva y las listas con viñetas.</span><span class="sxs-lookup"><span data-stu-id="b3615-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="b3615-153">tooadd un libro tooyour de sección de texto, usar hello **agregar texto** botón final Hola de libro de hello, o en parte inferior de Hola de cualquier sección.</span><span class="sxs-lookup"><span data-stu-id="b3615-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="b3615-154">Almacenamiento y uso compartido de libros con el equipo</span><span class="sxs-lookup"><span data-stu-id="b3615-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="b3615-155">Los libros se guardan en un recurso de Application Insights, ya sea en hello **Mis informes** sección que se encuentra tooyou privada o en hello **informes compartidos** sección que se encuentra accesible tooeveryone con acceso toohello recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b3615-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="b3615-156">tooview todos los libros de hello en el recurso de hello, haga clic en hello **abiertos** botón de barra de la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3615-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="b3615-157">un libro que está disponible actualmente en tooshare **Mis informes**:</span><span class="sxs-lookup"><span data-stu-id="b3615-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="b3615-158">Haga clic en **abiertos** en la barra de acciones de Hola</span><span class="sxs-lookup"><span data-stu-id="b3615-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="b3615-159">Haga clic en el botón "..." hello lateral libro Hola desea tooshare</span><span class="sxs-lookup"><span data-stu-id="b3615-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="b3615-160">Haga clic en **mover informes tooShared**.</span><span class="sxs-lookup"><span data-stu-id="b3615-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="b3615-161">tooshare un libro con un vínculo o por correo electrónico, haga clic en **recurso compartido** en la barra de acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3615-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="b3615-162">Tenga en cuenta que los destinatarios de vínculo de hello necesitan tener acceso a recursos toothis en libro Hola de hello tooview de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3615-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="b3615-163">ediciones toomake, los destinatarios necesitan al menos permisos de colaborador para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3615-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="b3615-164">toopin un libro de tooa vínculo tooan panel de Azure:</span><span class="sxs-lookup"><span data-stu-id="b3615-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="b3615-165">Haga clic en **abiertos** en la barra de acciones de Hola</span><span class="sxs-lookup"><span data-stu-id="b3615-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="b3615-166">Haga clic en el botón "..." hello lateral libro Hola desea toopin</span><span class="sxs-lookup"><span data-stu-id="b3615-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="b3615-167">Haga clic en **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="b3615-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3615-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3615-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3615-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3615-169">Next steps</span></span>
- <span data-ttu-id="b3615-170">uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="b3615-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="b3615-171">Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.</span><span class="sxs-lookup"><span data-stu-id="b3615-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="b3615-172">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="b3615-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="b3615-173">Embudos</span><span class="sxs-lookup"><span data-stu-id="b3615-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="b3615-174">Retención</span><span class="sxs-lookup"><span data-stu-id="b3615-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="b3615-175">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="b3615-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="b3615-176">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="b3615-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
