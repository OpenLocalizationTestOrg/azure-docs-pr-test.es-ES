---
title: "búsqueda de registros de aaaUpgrading Azure Log Analytics toonew | Documentos de Microsoft"
description: "lenguaje de consultas de análisis de registros nuevo Hola está casi aquí, y pueden participar en la vista previa pública de Hola.  En este artículo se describe las ventajas de Hola de nuevo lenguaje de Hola y cómo tooconvert el área de trabajo."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure

> [!NOTE]
> Actualización toohello nuevo lenguaje de consulta de análisis de registros está dando actualmente opcional demasiado tiempo[rampa ascendente en el nuevo lenguaje de hello](https://go.microsoft.com/fwlink/?linkid=856078).  

nuevo lenguaje de consulta de análisis de registros Hola está aquí, y deberá tooupgrade la ventaja de tootake de área de trabajo del mismo.  En este artículo se describe las ventajas de Hola de nuevo lenguaje de Hola y cómo tooconvert el área de trabajo.  Si no elige tooupgrade ahora, el área de trabajo continuará toooperate al igual que siempre, pero debe se convertirá automáticamente en una fecha posterior.  Recibirá una notificación con el tiempo suficiente cuando se fije dicha fecha.

Este artículo proporciona detalles sobre el nuevo lenguaje de Hola y el proceso de actualización de Hola.

## <a name="why-hello-new-language"></a>¿Por qué Hola nuevo idioma?
Somos conscientes de que hay dolor de cualquier transición, y solo se no estamos cambiar lenguaje de consulta de Hola para diversión Hola.  Hay varias razones que este cambio le proporcionará un valor significativo tooour clientes de análisis de registros.

- **Sencillez, pero eficacia.** nuevo lenguaje de Hello es más fácil toounderstand y tooSQL similar con construcciones más como natural idioma Hola heredado.
- **Lenguaje de canalización completa.**  nuevo lenguaje de Hello tiene más amplias capacidades de canalización de lenguaje heredado Hola.  Prácticamente cualquier salida puede ser tooanother canalizada comando toocreate consultas más complejas que eran posibles anteriormente.
- **Extracciones de campo de tiempo de búsqueda.**  nuevo lenguaje de Hello admite más avanzados campos de en tiempo de ejecución que calcula que idioma heredado Hola.  Puede utilizar cálculos complejos para los campos extendidos y, a continuación, utilice los campos de hello calculado para los comandos adicionales que se incluyen las combinaciones y agregaciones.
- **Combinaciones avanzadas.**  nuevo lenguaje de Hello proporciona combinaciones más avanzadas de lenguaje heredado Hola incluidas las tablas de toojoin de capacidad de hello en varios campos, use combinaciones internas y externas y participe en los campos extendidos.
- **Funciones de fecha y hora.**  nuevo lenguaje de Hello tiene más avanzadas funciones de fecha y hora de lenguaje heredado Hola.
- **Análisis inteligente.**  nuevo lenguaje de Hello ha avanzado patrones de tooevaluate de algoritmos en los conjuntos de datos y comparación distintos conjuntos de datos.
- **Portal de análisis avanzado.**  portal de análisis avanzado Hello ofrece características de análisis no está disponibles en el portal de análisis de registros de hello incluidos multilínea edición de consultas, visualizaciones adicionales y diagnósticos avanzados.
- **Coherencia con otras aplicaciones.**  Hola nuevo idioma hello y Portal de análisis avanzados ya se usan para el análisis en Application Insights.  Su implementación en Log Analytics ofrece coherencia entre los servicios de Azure.
- **Mejor integración con Power BI.** Las consultas en el nuevo lenguaje de hello pueden ser exportado tooPower BI Desktop, para que pueda utilizar sus capacidades de transformación de datos enriquecidos.
- **Y mucho más.** Consulte toohello [lenguaje de consultas de análisis de registro de Azure](https://docs.loganalytics.io) sitio para ver tutoriales sobre el nuevo lenguaje de Hola y detalles completos.


## <a name="when-can-i-upgrade"></a>¿Cuándo se puede actualizar?
actualización de Hola se lanzarán en todas las regiones de Azure para que estén disponible en algunas regiones antes que otras.  Sabrá cuando el área de trabajo es toobe disponible la próxima vez que vea pancarta Hola púrpura a través de la parte superior de hello del área de trabajo invitar a tooupgrade.

![Actualización 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>¿Qué ocurre cuando se actualiza?
Al convertir el área de trabajo, las búsquedas guardadas, las reglas de alerta y vistas que ha creado con el Diseñador de vistas de hello son toohello automáticamente convertido nuevo idioma.  Búsquedas incluidas en soluciones no se convierten automáticamente, pero está en su lugar, convertir en marcha Hola al abrirlos.  Esto es completamente transparente tooyou.

## <a name="can-i-go-back-after-i-upgrade"></a>¿Se puede revertir la actualización?
Cuando se actualiza, se realiza una copia de seguridad completa del área de trabajo que incluye una instantánea de las búsquedas guardadas, reglas de alertas y vistas.  Esto le permite toorestore el área de trabajo anterior si posteriormente debe así lo desea.

toorestore el área de trabajo heredado, vaya demasiado**configuración** en el área de trabajo y, a continuación, **resumen de la actualización**.  A continuación, puede seleccionar la opción de hello demasiado**restaurar el área de trabajo heredado**.  

![Restauración del área de trabajo heredada](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>¿Cómo debe realizar la actualización de hello?
Puede actualizar el área de trabajo cuando se verá banner de hello púrpura en la parte superior de hello del portal de Hola.  

1.  Iniciar el proceso de actualización de hello haciendo clic en el banner Hola púrpura que dice **obtener más información y actualizar**.<br>![Actualización 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Lea Hola obtener información adicional acerca de la actualización de hello en la página de información de actualización de Hola.<br>![Actualización 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Haga clic en **actualizar ahora** toostart actualización de Hola.<br>![Actualización 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Un cuadro de notificación en la esquina superior derecha de hello muestra el estado de saludo.<br>![Actualización 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  ¡Ya está!  Repase toohave de página de búsqueda de registros de toohello un vistazo a su área de trabajo actualizado.<br>![Actualización 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Si se produce un problema que hace que toofail actualización hello, pueden ir toohello [foro de discusión](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) y publique su pregunta o [crear una solicitud de soporte técnico](../azure-supportability/how-to-create-azure-support-request.md) de hello portal de Azure.

## <a name="how-do-i-learn-hello-new-language"></a>¿Cómo obtener nuevo lenguaje de hello?
Porque lo está usando varios servicios que hemos creado un [documentación del sitio externo toohost hello](https://docs.loganalytics.io/) nuevo lenguaje de Hola.  Esto incluye tutoriales, ejemplos y una toohelp de referencia completa que elabora toospeed. Puede ver un tutorial de nuevo lenguaje de hello en [Introducción a las consultas](https://go.microsoft.com/fwlink/?linkid=856078) y tener acceso a la referencia del lenguaje de hello en [idioma de consulta de análisis de registros](https://go.microsoft.com/fwlink/?linkid=856079).  

Si ya está familiarizado con hello heredado análisis de registro de lenguaje de consulta aunque, a continuación, se puede utilizar Hola lenguaje convertidor que se agrega el área de trabajo de tooyour como parte de la actualización de Hola.

Solo tiene que escribir la consulta heredada y, a continuación, haga clic en **convertir** toosee Hola traduce versión.  También puede, a continuación, haga clic con hello botón toorun Hola búsqueda o copiar y pegar Hola convertir consultas toouse en alguna otra parte, como una regla de alerta.

![Convertidor de lenguaje](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Pasos siguientes
- Desproteger un [tutorial en el nuevo lenguaje de hello](https://go.microsoft.com/fwlink/?linkid=856078).
- Recorrer un [tutorial sobre cómo usar el portal de la búsqueda de registro de hello](log-analytics-log-search-log-search-portal.md) con lenguaje de consultas nuevo Hola.
- Obtener una introducción toohello nueva [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587).
