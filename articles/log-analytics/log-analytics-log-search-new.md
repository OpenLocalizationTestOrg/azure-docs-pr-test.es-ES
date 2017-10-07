---
title: "búsquedas de aaaLog en análisis de registros de OMS | Documentos de Microsoft"
description: "Necesita un tooretrieve de búsqueda de registro en los datos de análisis de registros.  Este artículo describe cómo el nuevo registro de las búsquedas se usan en el análisis de registros y proporciona los conceptos que se deben toounderstand antes de crear uno."
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
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Descripción de las búsquedas de registros en Log Analytics

> [!NOTE]
> Este artículo describen las búsquedas de registros de análisis de registros de Azure mediante el lenguaje de consulta nueva Hola.  Puede obtener más información sobre el nuevo lenguaje de Hola y obtener Hola procedimiento tooupgrade el área de trabajo en [actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).  
>
> Si el área de trabajo no se ha actualizado toohello nuevo lenguaje de consulta, se debe hacer referencia demasiado[buscar datos mediante búsquedas de registros de análisis de registros](log-analytics-log-searches.md).

Necesita un tooretrieve de búsqueda de registro en los datos de análisis de registros.  Si se están analizando los datos en el portal de hello, configurar una regla de alerta toobe una notificación de una condición determinada o recuperar datos mediante Hola API de análisis de registros, usará un datos de hello toospecify de búsqueda de registro que desee.  Este artículo describe cómo se usan las búsquedas de registros en Log Analytics y proporciona los conceptos que debe comprender antes de crear una. Vea hello [pasos siguientes](#next-steps) sección para obtener más información sobre cómo crear y editar búsquedas de registros y de referencias en el lenguaje de consulta de Hola.

## <a name="where-log-searches-are-used"></a>Dónde se utilizan las búsquedas de registros

que va a usar búsquedas de registros de análisis de registros de diferentes maneras de Hola Hola siguientes:

- **Portales.** Puede realizar un análisis de datos interactivo en el repositorio de hello con hello [portal de la búsqueda de registro](log-analytics-log-search-log-search-portal.md) o hello [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587).  Esto le permite tooedit la consultar y analizar los resultados de hello en una variedad de formatos y visualizaciones.  Mayoría de las consultas que cree se iniciará en uno de los portales de hello y, a continuación, copia una vez que compruebe que funciona según lo previsto.
- **Reglas de alertas.** [Las reglas de alertas](log-analytics-alerts.md) identifican de manera proactiva los problemas de datos del área de trabajo.  Cada regla de alertas se basa en una búsqueda de registros que se ejecuta automáticamente a intervalos regulares.  resultados de Hello son toodetermine inspeccionado si se debe crear una alerta.
- **Vistas.**  Puede crear visualizaciones de toobe de datos incluidos en los paneles de usuario con [Diseñador de vistas](log-analytics-view-designer.md).  Búsquedas de registros proporcionan datos Hola utilizados por [iconos](log-analytics-view-designer-tiles.md) y [elementos de visualización](log-analytics-view-designer-parts.md) en cada vista.  Puede obtener detalles de elementos de visualización en búsqueda de registros tooperform portal un análisis más profundo en datos Hola Hola.
- **Exportación.**  Cuando se exportan datos desde tooExcel de área de trabajo de análisis de registros de Hola o [Power BI](log-analytics-powerbi.md), se crea un tooexport de datos de registro búsqueda toodefine Hola.
- **PowerShell.** Puede ejecutar un script de PowerShell desde una línea de comandos o un runbook de automatización de Azure que usa [AzureRmOperationalInsightsSearchResults Get](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve datos de análisis de registros.  Este cmdlet requiere una tooretrieve de datos de consulta toodetermine Hola.
- **API de Log Analytics.**  Hola [API de búsqueda de registro de análisis de registros](log-analytics-log-search-api.md) permite a cualquier cliente de la API de REST tooretrieve datos de área de trabajo de Hola.  solicitud de API de Hello incluye una consulta que se ejecuta en tooretrieve de datos de análisis de registros toodetermine Hola.

![Búsqueda de registros](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Organización de los datos de Log Analytics
Cuando se compila una consulta, primero debe determinar las tablas que tienen datos de Hola que está buscando. Cada [origen de datos](log-analytics-data-sources.md) y [solución](../operations-management-suite/operations-management-suite-solutions.md) almacena sus datos en tablas dedicadas en el área de trabajo de análisis de registros de Hola.  Documentación para cada origen de datos y la solución incluye nombre Hola Hola del tipo de datos que crea y una descripción de cada una de sus propiedades.     Muchas consultas sólo necesitarán datos de las tablas de una sola, pero otras personas pueden utilizar una variedad de opciones tooinclude datos de varias tablas.

![Tablas](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Escribir una consulta
Hola base del registro de las búsquedas en análisis de registros es [un lenguaje de consulta de una amplia](https://docs.loganalytics.io/) que le permite recuperar y analizar datos del repositorio de hello en una variedad de formas.  Este mismo idioma de consulta se utiliza para [Application Insights](../application-insights/app-insights-analytics.md).  Aprender cómo toowrite una consulta es crítico toocreating búsquedas de registros de análisis de registros.  Normalmente se empieza por consultas básicas y, a continuación, toouse de progreso más avanzadas funciones de los requisitos se vuelven más complejos.

estructura básica de Hola de una consulta es una tabla de origen seguida de una serie de operadores separados por un carácter de canalización `|`.  Puede encadenar varios operadores toorefine Hola de datos y realizar las funciones avanzadas.

Por ejemplo, suponga que desea toofind Hola top 10 equipos con hello mayoría de los eventos de error sobre Hola día pasado.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

O tal vez desee toofind equipos que no han tenido un latido en hello último día.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

¿Qué le parece un gráfico de líneas con la utilización del procesador de Hola para cada equipo de la semana pasada?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Puede ver en estos ejemplos de rápido que independientemente de su tipo de Hola de datos que está trabajando con, Hola estructura de consulta de hello es similar.  Puede dividirla en distintos pasos se envían Hola datos resultante de un comando mediante el siguiente comando de hello canalización toohello.

Para obtener documentación completa sobre el lenguaje de consulta de análisis de registros de Azure Hola incluidos tutoriales y referencia del lenguaje, vea hello [documentación del lenguaje de consulta de análisis de registros de Azure](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de hello [portales que utiliza toocreate y editar búsquedas de registros](log-analytics-log-search-portals.md).
- Desproteger un [tutorial sobre cómo escribir consultas](https://go.microsoft.com/fwlink/?linkid=856078) utilizando Hola nuevo lenguaje de consulta.
