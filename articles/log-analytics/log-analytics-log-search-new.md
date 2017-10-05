---
title: "Búsquedas de registros en Log Analytics de OMS | Microsoft Docs"
description: "Se requiere una búsqueda de registros para recuperar los datos de Log Analytics.  Este artículo describe cómo se usan las nuevas búsquedas de registros en Log Analytics y proporciona los conceptos que debe comprender antes de crear una."
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
ms.openlocfilehash: 0f27db7018e398f71a8d7bd0b86e643367b15875
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Descripción de las búsquedas de registros en Log Analytics

> [!NOTE]
> Este artículo describe las búsquedas de registros de Azure Log Analytics mediante el nuevo lenguaje de consulta.  Puede obtener más información sobre el nuevo lenguaje y conocer el procedimiento para actualizar el área de trabajo en [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md) (Actualización del área de trabajo de Azure Log Analytics al nuevo registro de búsquedas)///.  
>
> Si todavía no se ha actualizado el área de trabajo al nuevo lenguaje de consulta, vaya a [Búsqueda de datos mediante búsquedas de registros en Log Analytics](log-analytics-log-searches.md).

Se requiere una búsqueda de registros para recuperar los datos de Log Analytics.  Si está analizando los datos en el portal, configurando una regla de alertas para recibir una notificación sobre una condición determinada o recuperando datos mediante la API de Log Analytics, usará una búsqueda de registros para especificar los datos que desea.  Este artículo describe cómo se usan las búsquedas de registros en Log Analytics y proporciona los conceptos que debe comprender antes de crear una. Consulte la sección [Pasos siguientes](#next-steps) para más información sobre cómo crear y editar búsquedas de registros y para consultar referencias sobre el lenguaje de consulta.

## <a name="where-log-searches-are-used"></a>Dónde se utilizan las búsquedas de registros

Entre las distintas formas en que usará las búsquedas de registros en Log Analytics se incluyen las siguientes:

- **Portales.** Puede realizar un análisis de datos interactivo en el repositorio con el [portal de búsqueda de registros](log-analytics-log-search-log-search-portal.md) o el [portal avanzado de análisis](https://go.microsoft.com/fwlink/?linkid=856587).  Esto le permite modificar la consulta y analizar los resultados en una gran variedad de formatos y visualizaciones.  La mayoría de las consultas que cree se iniciarán en uno de los portales y, posteriormente, se copiarán una vez que compruebe que funcionan según lo previsto.
- **Reglas de alertas.** [Las reglas de alertas](log-analytics-alerts.md) identifican de manera proactiva los problemas de datos del área de trabajo.  Cada regla de alertas se basa en una búsqueda de registros que se ejecuta automáticamente a intervalos regulares.  Los resultados se inspeccionan para determinar si se debe crear una alerta.
- **Vistas.**  Puede crear visualizaciones de datos que se incluyan en los paneles de usuario con el [diseñador de vistas](log-analytics-view-designer.md).  Las búsquedas de registros proporcionan los datos utilizados por [iconos](log-analytics-view-designer-tiles.md) y [elementos de visualización](log-analytics-view-designer-parts.md) en cada vista.  Puede explorar en profundidad los elementos de visualización en el portal de búsqueda de registros para realizar análisis adicionales de los datos.
- **Exportación.**  Cuando exporte datos desde el área de trabajo de Log Analytics a Excel o [Power BI](log-analytics-powerbi.md), cree una búsqueda de registros para definir los datos que se van a exportar.
- **PowerShell.** Puede ejecutar un script de PowerShell desde una línea de comandos o un runbook de Azure Automation que utilice el cmdlet [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) para recuperar los datos de Log Analytics.  Este cmdlet requiere una consulta para determinar los datos que se van a recuperar.
- **API de Log Analytics.**  La [API de búsqueda de registros de Log Analytics](log-analytics-log-search-api.md) permite que cualquier cliente de API de REST recupere datos del área de trabajo.  La solicitud de API incluye una consulta que se ejecuta en Log Analytics para determinar los datos que se van a recuperar.

![Búsqueda de registros](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Organización de los datos de Log Analytics
Cuando compila una consulta, primero debe determinar las tablas que tienen los datos que está buscando. Cada [origen de datos](log-analytics-data-sources.md) y cada [solución](../operations-management-suite/operations-management-suite-solutions.md) almacena sus datos en tablas dedicadas en el área de trabajo de Log Analytics.  La documentación de cada origen de datos y solución incluye el nombre del tipo de datos que crea y una descripción de cada una de sus propiedades.     Muchas consultas solo necesitan datos de una sola tabla, pero otros usuarios pueden utilizar una variedad de opciones para incluir datos de varias tablas.

![Tablas](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Escribir una consulta
El núcleo del registro de búsquedas de Log Analytics es [un lenguaje de consulta amplio](https://docs.loganalytics.io/) que le permite recuperar y analizar datos desde el repositorio de varias formas.  Este mismo idioma de consulta se utiliza para [Application Insights](../application-insights/app-insights-analytics.md).  Aprender a escribir una consulta es fundamental para crear búsquedas de registros en Log Analytics.  Normalmente se empieza con consultas básicas para avanzar posteriormente a funciones más avanzadas a medida que sus requisitos se hacen más complejos.

La estructura básica de una consulta consiste en una tabla de origen seguida de una serie de operadores separados por un carácter de barra vertical `|`.  Puede encadenar varios operadores para refinar los datos y realizar funciones avanzadas.

Por ejemplo, suponga que desea buscar los diez equipos con más eventos de error del día anterior.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

O bien, quizá desee buscar los equipos que no han tenido un latido en el último día.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

¿Qué le parece un gráfico de líneas que muestre el uso del procesador por parte de cada equipo desde la semana pasada?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

En estos ejemplos rápidos se puede ver que, independientemente del tipo de datos con el que está trabajando, la estructura de la consulta es similar.  Puede dividirla en distintos pasos en los que los datos resultantes de un comando se envían a través de la canalización al siguiente comando.

Para obtener documentación completa sobre el lenguaje de consultas de Azure Log Analytics incluyendo tutoriales y referencia del lenguaje, consulte la [documentación del lenguaje de consulta de Azure Log Analytics](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de los [portales que puede utilizar para crear y editar búsquedas de registros](log-analytics-log-search-portals.md).
- Consulte un [tutorial sobre cómo escribir consultas](https://go.microsoft.com/fwlink/?linkid=856078) mediante el nuevo lenguaje de consulta.
