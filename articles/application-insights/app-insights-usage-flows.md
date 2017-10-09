---
title: "patrones de navegación de usuario aaaAnalyze con flujos de usuario de Azure Application Insights | Documentos de Microsoft"
description: "Analizar cómo los usuarios navegan entre páginas de Hola y las características de la aplicación web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Análisis de patrones de navegación del usuario mediante Flujos de usuarios de Application Insights

![Herramienta Flujos de usuarios de Application Insights](./media/app-insights-usage-flows/flows.png)

herramienta de usuario flujos de Hello muestra cómo los usuarios navegan entre páginas de Hola y las características del sitio. Resulta idónea para responder a preguntas del tipo:
* ¿Cómo salen los usuarios de una página del sitio?
* ¿En qué hacen clic los usuarios en una página del sitio?
* ¿Donde son Hola coloca que los usuarios la renovación de la mayor parte de su sitio?
* ¿Hay lugares donde los usuarios repetición Hola misma acción una y otra vez?

inicia la herramienta de usuario flujos de Hola de una vista de página inicial o eventos que se especifiquen. Esta vista de página o el evento personalizado, flujos de usuario dado Hola se muestra en las vistas de página y los eventos personalizados que se envían los usuarios inmediatamente después durante una sesión, dos pasos posteriormente, y así sucesivamente. Aparecen líneas de varios grosores que muestran cuántas veces han seguido cada ruta los usuarios. Nodos especiales "Finalizó la sesión" Mostrar cuántos usuarios no envían ningún vistas de página o eventos personalizados después de hello anterior, resaltado que los usuarios dejan probablemente su sitio.



> [!NOTE]
> El recurso de Application Insights debe contener las vistas de página o herramienta de usuario flujos de eventos personalizados toouse Hola. [Obtenga información acerca de cómo tooset la página de aplicación toocollect vistas automáticamente con hello Application Insights JavaScript SDK](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Empiece por elegir una vista de página inicial o un evento personalizado

![Elegir un evento inicial para Flujos de usuarios](./media/app-insights-usage-flows/flows-initial-event.png)

tooget inició responder a preguntas con una herramienta de usuario flujos de hello, elija una vista de página inicial o el evento personalizado tooserve como punto de partida para la visualización de Hola de hello:
1. Haga clic en el vínculo de Hola Hola "¿qué hacer a los usuarios una vez...?" título, o haga clic en el botón de edición de Hola. 
2. Seleccione una vista de página o un evento personalizado en lista desplegable de Hola "Evento inicial".
3. Haga clic en "Crear grafo".

columna de "Paso 1" Hello de visualización de hello muestra lo que los usuarios con más frecuencia hizo justo después de evento inicial de hello, ordenados de arriba a abajo desde tooleast más frecuente. Hola "Paso 2" y las columnas siguientes muestran lo que los usuarios ha sido a partir de ahí, crear una imagen de todos los usuarios de maneras de hello han navegado a través del sitio.

De forma predeterminada, herramienta de usuario flujos de hello muestrea de forma aleatoria solo Hola últimas 24 horas de vistas de página y el evento personalizado desde su sitio. Puede aumentar el intervalo de tiempo de Hola y cambiar Hola equilibrio entre rendimiento y precisión para el muestreo aleatorio en el menú de edición de Hola.

Si algunas de las vistas de página hello y eventos personalizados no están tooyou relevante, haga clic en "X" hello en nodos de hello desea toohide. Una vez que haya seleccionado los nodos de Hola que desea toohide, haga clic en botón de "Crear gráfico" hello por debajo de la visualización de Hola. toosee todos los nodos de hello ha ocultado, haga clic en el botón de edición de Hola y mire la sección de "Excluir eventos" Hola.

Si las vistas de página o eventos personalizados faltan, esperar toosee en la visualización de hello:
* Compruebe la sección "Excluir eventos" hello en el menú de edición de Hola.
* Usar control en el "Nivel de detalle" Hola Hola Editar menú tooinclude menos frecuente de eventos de visualización de Hola.
* Si la vista de página de Hola o eventos personalizados que se espera que se envían con poca frecuencia por los usuarios, pruebe cada vez mayor intervalo de tiempo de Hola de visualización de hello en el menú de edición de Hola.
* Asegúrese de vista de página de hello seguro o eventos personalizados que se espera que se configura toobe recopilado por hello Application Insights SDK en el código fuente de Hola de su sitio. [Obtenga más información sobre la recopilación de eventos personalizados](app-insights-api-custom-events-metrics.md).

Si desea que toosee más pasos de visualización de hello, Hola de uso "Número de pasos" control deslizante en hello menú Edición.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Después de visitar una página o una característica, ¿a dónde van los usuarios y dónde hacen clic?

![Usar flujos de usuario toounderstand donde los usuarios hacer clic](./media/app-insights-usage-flows/flows-one-step.png)

Si el evento inicial es una vista de página, Hola primera columna ("paso 1") de visualización de hello es un toounderstand de forma rápida qué usuarios ha inmediatamente después de visitar la página de Hola. Intente abrir el sitio en una visualización de usuario flujos de ventana siguiente toohello. Compare sus expectativas de cómo los usuarios interactúan con lista de hello página toohello de eventos en la columna de "Paso 1" Hola. A menudo, puede ser un elemento de interfaz de usuario en las páginas de Hola que parece tooyour insignificante equipo entre Hola usados en la página de Hola. Puede ser un buen punto de partida para el sitio de tooyour de mejoras de diseño.

Si el evento inicial es un evento personalizado, primera columna de hello muestra lo que los usuarios que hizo justo después de realizar esa acción. Al igual que con las vistas de página, tenga en cuenta si Hola observados coincide con el comportamiento de los usuarios expectativas y objetivos de su equipo. Si el evento inicial seleccionado es "Added elemento tooShopping Cart", por ejemplo, busque toosee si "Go tooCheckout" y "Completado la compra" aparecen en la visualización de hello poco después. Si el comportamiento de usuario es muy diferente de sus expectativas, use Hola visualización toounderstand cómo los usuarios están obteniendo "capturados" por diseño actual de su sitio.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>¿Donde son Hola coloca que los usuarios la renovación de la mayor parte de su sitio?

Inspección para los nodos "Finalizó la sesión" que aparecen arriba de alta en una columna de visualización de hello, especialmente al principio de un flujo. Esto significa que muchos usuarios probablemente creados desde su sitio una vez siguiente Hola anterior ruta de acceso de las páginas y las interacciones de la interfaz de usuario. En algunas ocasiones, aunque el abandono es previsible, como, por ejemplo, después de completar una compra en un sitio de comercio electrónico, este suele ser indicativo de problemas de diseño, bajo rendimiento u otras cuestiones mejorables.

Tenga en cuenta que los nodos "Fin de la sesión" se basan únicamente en la telemetría recopilada por este recurso de Application Insights. Si Application Insights no reciba datos de telemetría para ciertas las interacciones del usuario, los usuarios podrían todavía ha interactuado con su sitio en los casos indicados después de herramienta de usuario flujos de hello dice Hola sesión ha finalizado.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>¿Hay lugares donde los usuarios repetición Hola misma acción una y otra vez?

Busque una vista de página o un evento personalizado que se repite por muchos usuarios a través de los pasos subsiguientes de visualización de Hola. Normalmente, esto significa que los usuarios están realizando acciones repetitivas en su sitio. Si encuentra repetición, piense en cambiar el diseño de Hola de su sitio o la adición de repetición de tooreduce funcionalidad nueva. Por ejemplo, agregue la funcionalidad de edición en masa si observa que los usuarios realizan acciones repetitivas en cada fila de un elemento de tabla.

## <a name="common-questions"></a>Preguntas frecuentes

### <a name="why-do-steps-appear-disconnected"></a>¿Por qué aparecen desconectados los pasos?

![Flujos de usuarios con pasos desconectados](./media/app-insights-usage-flows/flows-disconnected.png)

Si se desconectan pasos (columnas) de una visualización de flujos de usuario, significa que ninguna de las rutas de acceso de hello realizadas por los usuarios entre los pasos de hello eran lo suficientemente frecuente toobe que se muestra. tooshow menos eventos frecuentes de visualización de Hola para que aparezcan conectadas, pasos de hello Ajustar control deslizante de "Nivel de detalle" hello en el menú de edición de Hola.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>¿Hola inicial representan Hola primera hora Hola evento aparece en una sesión o siempre que aparece en una sesión?

evento inicial de Hello en la visualización de hello representa solo Hola primera vez que un usuario envía esa vista de página o el evento personalizado durante una sesión. Si los usuarios pueden enviar evento inicial de hello varias veces en una sesión, columna "Paso 1" de hello solo muestra el comportan de los usuarios después de hello *primer* instancia de evento inicial, no todas las instancias.

## <a name="next-steps"></a>Pasos siguientes

* [Información general del uso](app-insights-usage-overview.md)
* [Usuarios, sesiones y eventos](app-insights-usage-segmentation.md)
* [Retención](app-insights-usage-retention.md)
* [Agregar eventos personalizados tooyour aplicación](app-insights-api-custom-events-metrics.md)
