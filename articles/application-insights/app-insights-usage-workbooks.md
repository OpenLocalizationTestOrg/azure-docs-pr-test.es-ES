---
title: "Investigación y uso compartido de datos de uso con libros interactivos en Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="e2987-103">Investigación y uso compartido de datos de uso con libros interactivos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2987-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="e2987-104">Los libros combinan las visualizaciones de datos de [Azure Application Insights](app-insights-overview.md), las [consultas de Analytics](app-insights-analytics.md) y texto en documentos interactivos.</span><span class="sxs-lookup"><span data-stu-id="e2987-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="e2987-105">Otros miembros del equipo con acceso al mismo recurso de Azure pueden editar los libros.</span><span class="sxs-lookup"><span data-stu-id="e2987-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="e2987-106">Esto significa que las consultas y los controles utilizados para crear un libro están disponibles para las demás personas que leen el libro, lo que facilita su exploración, ampliación y la búsqueda de errores.</span><span class="sxs-lookup"><span data-stu-id="e2987-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="e2987-107">Los libros son útiles en escenarios como:</span><span class="sxs-lookup"><span data-stu-id="e2987-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="e2987-108">Exploración del uso de la aplicación cuando no conoce de antemano las métricas de interés: número de usuarios, tasas de retención, tasas de conversión, etc. A diferencia de otras herramientas de análisis de uso de Application Insights, los libros le permiten combinar varios tipos de visualizaciones y análisis, lo cual los hace idóneos para este tipo de exploración de forma libre.</span><span class="sxs-lookup"><span data-stu-id="e2987-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="e2987-109">A la hora de explicar al equipo el rendimiento de una característica recientemente publicada, mostrando recuentos de usuarios para las interacciones principales y otras métricas.</span><span class="sxs-lookup"><span data-stu-id="e2987-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="e2987-110">Uso compartido de los resultados de un experimento A o B de la aplicación con otros miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="e2987-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="e2987-111">Puede explicar los objetivos del experimento con texto y luego mostrar cada métrica de uso y la consulta de Analytics que se usa para evaluar el experimento, junto con indicadores claros sobre si cada métrica está por encima o por debajo del objetivo.</span><span class="sxs-lookup"><span data-stu-id="e2987-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="e2987-112">Notificación del impacto de una interrupción del servicio en el uso de la aplicación, combinación de datos, explicación del texto y análisis de los pasos siguientes para evitar más interrupciones en el futuro.</span><span class="sxs-lookup"><span data-stu-id="e2987-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="e2987-113">El recurso de Application Insights debe contener vistas de página o eventos personalizados para utilizar los libros.</span><span class="sxs-lookup"><span data-stu-id="e2987-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="e2987-114">[Aprenda a configurar la aplicación para que recopile vistas de página automáticamente con el SDK de JavaScript de Application Insights](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e2987-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="e2987-115">Edición, reorganización, clonación y eliminación de secciones de libro</span><span class="sxs-lookup"><span data-stu-id="e2987-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="e2987-116">Un libro está compuesto de secciones: visualizaciones de uso que se pueden editar independientemente, gráficos, tablas, texto o resultados de consultas de Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2987-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="e2987-117">Para editar el contenido de una sección de un libro, haga clic en el botón **Editar** situado en la parte inferior derecha de la sección del libro.</span><span class="sxs-lookup"><span data-stu-id="e2987-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Controles de edición de secciones de libros de Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="e2987-119">Cuando haya terminado de editar una sección, haga clic en **Edición finalizada** en la esquina inferior izquierda de la sección.</span><span class="sxs-lookup"><span data-stu-id="e2987-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="e2987-120">Para crear un duplicado de una sección, haga clic en el icono **Clone this section** (Clonar este sección).</span><span class="sxs-lookup"><span data-stu-id="e2987-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="e2987-121">La creación de secciones duplicadas es una forma ideal de iterar una consulta sin perder las iteraciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="e2987-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="e2987-122">Para mover hacia arriba una sección de un libro, haga clic en el icono **Subir** o **Bajar**.</span><span class="sxs-lookup"><span data-stu-id="e2987-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="e2987-123">Para eliminar una sección de forma permanente, haga clic en el icono **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="e2987-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="e2987-124">Incorporación de secciones de visualización de datos de uso</span><span class="sxs-lookup"><span data-stu-id="e2987-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="e2987-125">Los libros ofrecen cuatro tipos de visualizaciones de análisis de uso integradas.</span><span class="sxs-lookup"><span data-stu-id="e2987-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="e2987-126">Cada una de ellas responde a una pregunta habitual acerca del uso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2987-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="e2987-127">Para agregar tablas y gráficos distintos a estas cuatro secciones, agregue secciones de consultas de Analytics (consulte a continuación).</span><span class="sxs-lookup"><span data-stu-id="e2987-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="e2987-128">Para agregar una sección de Usuarios, Sesiones, Eventos o Retención al libro, use el botón **Agregar usuarios** o el botón correspondiente situado en la parte inferior del libro, o en la parte inferior de cualquier sección.</span><span class="sxs-lookup"><span data-stu-id="e2987-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Sección Usuarios en los libros](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="e2987-130">Las secciones **Usuarios** dan respuesta a la pregunta "¿cuántos usuarios vieron una página determinada o utilizaron alguna característica de mi sitio?"</span><span class="sxs-lookup"><span data-stu-id="e2987-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="e2987-131">Las secciones **Sesiones** dan respuesta a la pregunta "¿cuántas sesiones emplearon los usuarios para ver una página determinada o usar alguna característica de mi sitio?"</span><span class="sxs-lookup"><span data-stu-id="e2987-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="e2987-132">Las secciones **Eventos** dan respuesta a la pregunta "¿cuántas veces vieron los usuarios una página determinada o utilizaron alguna característica de mi sitio?"</span><span class="sxs-lookup"><span data-stu-id="e2987-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="e2987-133">Cada uno de estos tres tipos de sección ofrece los mismos conjuntos de controles y visualizaciones:</span><span class="sxs-lookup"><span data-stu-id="e2987-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="e2987-134">Más información sobre la edición de las secciones Usuarios, Sesiones y Eventos</span><span class="sxs-lookup"><span data-stu-id="e2987-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="e2987-135">Active o desactive el gráfico principal, las cuadrículas de histograma, los análisis automáticos y las visualizaciones de los usuarios de ejemplo mediante las casillas **Mostrar gráfico**, **Mostrar cuadrícula**, **Mostrar Insights** y **Ejemplo de estos usuarios** situadas en la parte superior de cada sección.</span><span class="sxs-lookup"><span data-stu-id="e2987-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Sección Retención en los libros](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="e2987-137">Las secciones **Retención** dan respuesta a la pregunta: "De las personas que vieron una página determinada o usaron alguna característica en un día o semana concretos, ¿cuántos regresaron otro día o semana posteriores?"</span><span class="sxs-lookup"><span data-stu-id="e2987-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="e2987-138">Más información acerca de la edición de las secciones de retención</span><span class="sxs-lookup"><span data-stu-id="e2987-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="e2987-139">Active o desactive el gráfico de retenciones totales mediante la casilla **Mostrar gráfico de retenciones totales** situada en la parte superior de la sección.</span><span class="sxs-lookup"><span data-stu-id="e2987-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="e2987-140">Incorporación de secciones de análisis de Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2987-140">Adding Application Insights Analytics sections</span></span>

![Sección de análisis en los libros](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="e2987-142">Para agregar una sección de consultas de análisis de Application Insights en el libro, use el botón **Agregar consulta de análisis** situado en la parte inferior del libro o en la parte inferior de cualquier sección.</span><span class="sxs-lookup"><span data-stu-id="e2987-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="e2987-143">Las secciones de consulta de análisis le permiten agregar consultas arbitrarias sobre los datos de Application Insights a los libros.</span><span class="sxs-lookup"><span data-stu-id="e2987-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="e2987-144">Esta flexibilidad significa que las secciones de consultas de análisis pueden ser el medio para responder a preguntas sobre el sitio distintas a las de las cuatro categorías mencionadas anteriormente de usuarios, sesiones, eventos y retención, como:</span><span class="sxs-lookup"><span data-stu-id="e2987-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="e2987-145">¿Cuántas excepciones produjo el sitio durante un período de tiempo equivalente al de un declive del uso?</span><span class="sxs-lookup"><span data-stu-id="e2987-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="e2987-146">¿Cuál fue la distribución de los tiempos de carga de página de los usuarios que vieron alguna página?</span><span class="sxs-lookup"><span data-stu-id="e2987-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="e2987-147">¿Cuántos usuarios vieron un conjunto de páginas determinado de su sitio, pero no otro?</span><span class="sxs-lookup"><span data-stu-id="e2987-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="e2987-148">Esto puede ser útil para comprender si tiene clústeres de usuarios que utilizan distintos subconjuntos de funcionalidad del sitio (use el operador `join` con el modificador `kind=leftanti` en el lenguaje de consulta de Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="e2987-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="e2987-149">Use la [referencia de lenguaje de consulta de Log Analytics](https://docs.loganalytics.io/) para más información sobre la escritura de consultas.</span><span class="sxs-lookup"><span data-stu-id="e2987-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="e2987-150">Adición de texto y secciones de Markdown</span><span class="sxs-lookup"><span data-stu-id="e2987-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="e2987-151">La adición de títulos, explicaciones y comentarios a los libros le ayuda a convertir un conjunto de tablas y gráficos en una descripción.</span><span class="sxs-lookup"><span data-stu-id="e2987-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="e2987-152">Las secciones de texto de los libros son compatibles con la [sintaxis de Markdown](https://daringfireball.net/projects/markdown/) para dar formato a los textos como títulos, negrita, cursiva y listas con viñetas.</span><span class="sxs-lookup"><span data-stu-id="e2987-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="e2987-153">Para agregar una sección de texto al libro, use el botón **Agregar texto** situado en la parte inferior del libro o en la parte inferior de cualquier sección.</span><span class="sxs-lookup"><span data-stu-id="e2987-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="e2987-154">Almacenamiento y uso compartido de libros con el equipo</span><span class="sxs-lookup"><span data-stu-id="e2987-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="e2987-155">Los libros se guardarán en un recurso de Application Insights, ya sea en la sección privada de **Mis informes** o en la sección **Informes compartidos** a la que pueden acceder todos los usuarios con acceso al recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e2987-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="e2987-156">Para ver todos los libros del recurso, haga clic en el botón **Abrir** de la barra de acciones.</span><span class="sxs-lookup"><span data-stu-id="e2987-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="e2987-157">Para compartir un libro que está actualmente en **Mis informes**:</span><span class="sxs-lookup"><span data-stu-id="e2987-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="e2987-158">Haga clic en **Abrir** en la barra de acciones</span><span class="sxs-lookup"><span data-stu-id="e2987-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="e2987-159">Haga clic en el botón "..." situado junto al libro que desea compartir</span><span class="sxs-lookup"><span data-stu-id="e2987-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="e2987-160">Haga clic en **Move to Shared Reports** (Mover a informes compartidos).</span><span class="sxs-lookup"><span data-stu-id="e2987-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="e2987-161">Para compartir un libro con un vínculo o por correo electrónico, haga clic en **Compartir** en la barra de acciones.</span><span class="sxs-lookup"><span data-stu-id="e2987-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="e2987-162">Tenga en cuenta que los destinatarios del vínculo necesitarán acceder a este recurso en Azure Portal para ver el libro.</span><span class="sxs-lookup"><span data-stu-id="e2987-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="e2987-163">Para realizar ediciones, los destinatarios necesitan al menos permisos de colaborador para el recurso.</span><span class="sxs-lookup"><span data-stu-id="e2987-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="e2987-164">Para anclar un vínculo a un libro en un panel de Azure:</span><span class="sxs-lookup"><span data-stu-id="e2987-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="e2987-165">Haga clic en **Abrir** en la barra de acciones</span><span class="sxs-lookup"><span data-stu-id="e2987-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="e2987-166">Haga clic en el botón "..." situado junto al libro que desea anclar</span><span class="sxs-lookup"><span data-stu-id="e2987-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="e2987-167">Haga clic en **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="e2987-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2987-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2987-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2987-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2987-169">Next steps</span></span>
- <span data-ttu-id="e2987-170">Para habilitar las experiencias de uso, empiece por enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [vistas de páginas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="e2987-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="e2987-171">Si ya ha enviado eventos personalizados o vistas de página, explore las herramientas de uso para obtener información sobre cómo los usuarios utilizan el servicio.</span><span class="sxs-lookup"><span data-stu-id="e2987-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="e2987-172">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="e2987-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="e2987-173">Embudos</span><span class="sxs-lookup"><span data-stu-id="e2987-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="e2987-174">Retención</span><span class="sxs-lookup"><span data-stu-id="e2987-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="e2987-175">Flujos de usuario</span><span class="sxs-lookup"><span data-stu-id="e2987-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="e2987-176">Adición de contexto de usuario</span><span class="sxs-lookup"><span data-stu-id="e2987-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
