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
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Investigación y uso compartido de datos de uso con libros interactivos en Application Insights

Los libros combinan las visualizaciones de datos de [Azure Application Insights](app-insights-overview.md), las [consultas de Analytics](app-insights-analytics.md) y texto en documentos interactivos. Los libros son puede ser editados por otros miembros del equipo con acceso toohello mismo recurso de Azure. Esto significa hello las consultas y los controles utilizado toocreate un libro son tooother disponibles cuando los usuarios visiten libro hello, haciéndolos tooexplore fácil, ampliar y buscar errores.

Los libros son útiles en escenarios como:

* Explorar el uso de saludo de la aplicación si no conoce de antemano las métricas de Hola de interés: número de usuarios, tasas de retención, las tasas de conversión, etcetera. A diferencia de otras herramientas de análisis de uso de Application Insights, los libros le permiten combinar varios tipos de visualizaciones y análisis, lo cual los hace idóneos para este tipo de exploración de forma libre.
* Explicar equipo tooyour el rendimiento de una característica recientemente publicada, por el usuario que muestra los recuentos de interacciones de claves y otras métricas.
* Uso compartido de resultados de Hola de una A / B experimentar en su aplicación con otros miembros del equipo. Puede explicar objetivos de Hola para hello experimentar con texto, a continuación muestran cada métrica de uso y consulta de análisis usa experimento de hello tooevaluate, junto con la espera de llamada clara de si cada métrica era por encima o por debajo-las destino.
* Impacto de Hola de una interrupción de informes sobre el uso de saludo de la aplicación, la combinación de datos, texto de explicación y una explicación de las interrupciones de tooprevent pasos siguientes Hola futuras.

> [!NOTE]
> El recurso de Application Insights debe contener las vistas de página o los libros de toouse de eventos personalizados. [Obtenga información acerca de cómo tooset la página de aplicación toocollect vistas automáticamente con hello Application Insights JavaScript SDK](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Edición, reorganización, clonación y eliminación de secciones de libro

Un libro está compuesto de secciones: visualizaciones de uso que se pueden editar independientemente, gráficos, tablas, texto o resultados de consultas de Analytics.

contenido de hello tooedit de una sección del libro, haga clic en hello **editar** botón siguiente y toohello derecha de la sección del libro de Hola.

![Controles de edición de secciones de libros de Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. Cuando haya terminado editar una sección, haga clic en **realiza edición** en esquina Hola inferior izquierda de la sección de Hola.

2. toocreate un duplicado de una sección, haga clic en hello **clonar esta sección** icono. Crear secciones duplicadas es un tooiterate tooway excelente en una consulta sin perder las iteraciones anteriores.

3. toomove hacia arriba una sección en un libro, haga clic en hello **se desplazan hacia arriba** o **Bajar** icono.

4. tooremove una sección de forma permanente, haga clic en hello **quitar** icono.

## <a name="adding-usage-data-visualization-sections"></a>Incorporación de secciones de visualización de datos de uso

Los libros ofrecen cuatro tipos de visualizaciones de análisis de uso integradas. Cada uno de ellos responde a una pregunta común acerca del uso de saludo de la aplicación. tooadd tablas y gráficos que no sea de estos cuatro secciones, agregue secciones de consultas de análisis (ver abajo).

tooadd a los usuarios, sesiones, eventos o retención sección tooyour libro, use hello **agregar usuarios** o en otro botón correspondiente en parte inferior de Hola de libro de Hola o en parte inferior de Hola de cualquier sección.

![Sección Usuarios en los libros](./media/app-insights-usage-workbooks/users-section.png)

Las secciones **Usuarios** dan respuesta a la pregunta "¿cuántos usuarios vieron una página determinada o utilizaron alguna característica de mi sitio?"

Las secciones **Sesiones** dan respuesta a la pregunta "¿cuántas sesiones emplearon los usuarios para ver una página determinada o usar alguna característica de mi sitio?"

Las secciones **Eventos** dan respuesta a la pregunta "¿cuántas veces vieron los usuarios una página determinada o utilizaron alguna característica de mi sitio?"

Cada uno de estos tipos de tres sección ofrece Hola mismos conjuntos de controles y visualizaciones:

* [Más información sobre la edición de las secciones Usuarios, Sesiones y Eventos](app-insights-usage-segmentation.md)
* Alternar gráfico principal de hello, cuadrículas de histograma, visión automática y visualizaciones de los usuarios de ejemplo con hello **Mostrar gráfico**, **Mostrar cuadrícula**, **mostrar visión**y **Ejemplo de estos usuarios** casillas de verificación en la parte superior de Hola de cada sección.

![Sección Retención en los libros](./media/app-insights-usage-workbooks/retention-section.png)

Las secciones **Retención** dan respuesta a la pregunta: "De las personas que vieron una página determinada o usaron alguna característica en un día o semana concretos, ¿cuántos regresaron otro día o semana posteriores?"

* [Más información acerca de la edición de las secciones de retención](app-insights-usage-retention.md)
* Alternar Hola opcionales retención total del gráfico mediante hello **Mostrar gráfico de retención global** casilla situada en la parte superior de Hola de sección Hola.

## <a name="adding-application-insights-analytics-sections"></a>Incorporación de secciones de análisis de Application Insights

![Sección de análisis en los libros](./media/app-insights-usage-workbooks/analytics-section.png)

tooadd un libro de tooyour sección de consulta de análisis de visión de aplicaciones, usar hello **consulta de análisis de agregar** botón final Hola de libro de hello, o en parte inferior de Hola de cualquier sección.

Las secciones de consulta de análisis le permiten agregar consultas arbitrarias sobre los datos de Application Insights a los libros. Esta flexibilidad significa que las secciones de consultas de análisis deben ser su go-toofor responder a preguntas sobre el sitio que no sea de hello cuatro mencionado anteriormente para los usuarios, sesiones, eventos y retención, como:

* ¿Cuántas excepciones hizo su throw sitio durante Hola mismo período como un descenso en cuanto al uso de tiempo?
* ¿Cuál era la distribución de Hola de tiempos de carga de página para los usuarios que vean algunos página?
* ¿Cuántos usuarios vieron un conjunto de páginas determinado de su sitio, pero no otro? Esto puede resultar útil toounderstand si tiene clústeres de los usuarios que utilizan distintos subconjuntos de funcionalidad de su sitio (usar hello `join` operador con hello `kind=leftanti` modificador Hola lenguaje de consultas de análisis de registros).

Hola de uso [referencia del lenguaje de consulta de análisis de registro](https://docs.loganalytics.io/) toolearn más acerca de cómo escribir consultas.

## <a name="adding-text-and-markdown-sections"></a>Adición de texto y secciones de Markdown

Agregar títulos, explicaciones y libros de comentarios tooyour le ayuda a convertir un conjunto de tablas y gráficos en una descripción. Las secciones de texto en los libros admiten hello [sintaxis de Markdown](https://daringfireball.net/projects/markdown/) de formato de texto, como encabezados, negrita, cursiva y las listas con viñetas.

tooadd un libro tooyour de sección de texto, usar hello **agregar texto** botón final Hola de libro de hello, o en parte inferior de Hola de cualquier sección.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Almacenamiento y uso compartido de libros con el equipo

Los libros se guardan en un recurso de Application Insights, ya sea en hello **Mis informes** sección que se encuentra tooyou privada o en hello **informes compartidos** sección que se encuentra accesible tooeveryone con acceso toohello recurso de Application Insights. tooview todos los libros de hello en el recurso de hello, haga clic en hello **abiertos** botón de barra de la acción de Hola.

un libro que está disponible actualmente en tooshare **Mis informes**:

1. Haga clic en **abiertos** en la barra de acciones de Hola
2. Haga clic en el botón "..." hello lateral libro Hola desea tooshare
3. Haga clic en **mover informes tooShared**.

tooshare un libro con un vínculo o por correo electrónico, haga clic en **recurso compartido** en la barra de acciones de Hola. Tenga en cuenta que los destinatarios de vínculo de hello necesitan tener acceso a recursos toothis en libro Hola de hello tooview de portal de Azure. ediciones toomake, los destinatarios necesitan al menos permisos de colaborador para el recurso de Hola.

toopin un libro de tooa vínculo tooan panel de Azure:

1. Haga clic en **abiertos** en la barra de acciones de Hola
2. Haga clic en el botón "..." hello lateral libro Hola desea toopin
3. Haga clic en **toodashboard Pin**.

## <a name="next-steps"></a>Pasos siguientes

## <a name="next-steps"></a>Pasos siguientes
- uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.
    - [Usuarios, sesiones, eventos](app-insights-usage-segmentation.md)
    - [Embudos](usage-funnels.md)
    - [Retención](app-insights-usage-retention.md)
    - [Flujos de usuario](app-insights-usage-flows.md)
    - [Adición de contexto de usuario](app-insights-usage-send-user-context.md)
    
