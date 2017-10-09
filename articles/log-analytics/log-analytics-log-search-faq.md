---
title: "Preguntas más frecuentes sobre la búsqueda de registros nuevos de aaaLog análisis | Documentos de Microsoft"
description: "Este artículo proporciona las preguntas más frecuentes sobre actualización de Hola de nuevo lenguaje de consulta de análisis de registros toohello."
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
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Problemas conocidos y preguntas frecuentes sobre la nueva búsqueda de registros de Log Analytics

Este artículo incluye las preguntas más frecuentes y problemas conocidos relacionados con la actualización de Hola de [toohello de análisis de registros nuevo lenguaje de consulta](log-analytics-log-search-upgrade.md).  Lea este artículo completo antes de realizar tooupgrade de decisión de hello en el área de trabajo.


## <a name="alerts"></a>Alertas

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Pregunta: Tengo una gran cantidad de reglas de alertas. ¿Necesito toocreate ellas nuevo en hello nuevo idioma después de actualizar?  
No, las reglas de alertas están nuevo lenguaje de búsqueda toohello convertido automáticamente durante la actualización.  


## <a name="computer-groups"></a>Grupos de equipos

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Pregunta: Estoy obteniendo errores al tratar de grupos de equipos de toouse.  ¿Se ha modificado su sintaxis?
Sí, la sintaxis de Hola para usar el equipo hace cambios estén condensados cuando se actualiza el área de trabajo.  Consulte [Grupos de equipos en búsquedas de registros en Log Analytics](log-analytics-computer-groups.md) para obtener información detallada.

### <a name="known-issue-groups-imported-from-active-directory"></a>Problema conocido: Grupos importados desde Active Directory
Actualmente no puede crear una consulta que use un grupo de equipos importados desde Active Directory.  Para solucionar este problema hasta que se corrija este problema, cree un nuevo grupo de equipos mediante el grupo de Active Directory de hello importado y, a continuación, usar ese grupo nuevo en la consulta.

Un toocreate de consulta de ejemplo un nuevo grupo de equipos que incluye un grupo de Active Directory importado es como sigue:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Paneles

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Pregunta: ¿Puedo usar paneles aún en un área de trabajo actualizada?
Puede seguir los iconos que ha agregado demasiado toouse**Mi panel** antes de que se actualizó el área de trabajo, pero no puede editar los iconos ni agregar otros nuevos.  Puede continuar toocreate y editar vistas con [Diseñador de vistas](log-analytics-view-designer.md) y también se crean paneles en hello portal de Azure.


## <a name="log-searches"></a>Búsqueda de registros

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Pregunta: He guardado búsquedas fuera de mi área de trabajo actualizada. ¿Convertirlos toohello nuevo lenguaje de búsqueda automáticamente?
Puede utilizar herramienta de conversión de idioma de hello en tooconvert de página de búsqueda de registro de hello en cada uno de ellos.  Varias búsquedas sin actualizar el área de trabajo de hello no hay ninguna conversión de tooautomatically de método.

### <a name="question-why-are-my-query-results-not-sorted"></a>Pregunta: ¿Por qué los resultados de la consulta no están ordenados?
Resultados no se ordenan de forma predeterminada en el nuevo lenguaje de consulta Hola.  Hola de uso [operador sort](https://go.microsoft.com/fwlink/?linkid=856079) toosort los resultados por una o varias propiedades.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Problema conocido: Los resultados de la búsqueda de una lista pueden incluir propiedades sin datos
Los resultados de la búsqueda de registros de una lista pueden mostrar propiedades sin datos.  Tooupgrade anterior, estas propiedades no estén incluidas.  Este problema se corregirá para que no se muestren las propiedades vacías.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Problema conocido: Al seleccionar el valor de un gráfico, no se muestran resultados detallados
Tooupgrade anterior, cuando se selecciona un valor en un gráfico, devolvería una lista detallada de los registros que coincidan con el valor de hello seleccionado.  Después de la actualización, se devuelve solo Hola resumidos línea única.  Actualmente se está investigando este problema.

## <a name="log-search-api"></a>API de búsqueda de registros

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Pregunta: Hola API de búsqueda de registros se actualizan después de actualizar?
Hola [API de búsqueda de registros](log-analytics-log-search-api.md) aún no se ha actualizado toohello nuevo lenguaje de búsqueda.  Continuar el lenguaje de consulta heredado de toouse Hola con esta API, incluso después de actualizar el área de trabajo.  Documentación actualizada estará disponible para la API de búsqueda de registros de hello cuando se actualiza.


## <a name="portals"></a>Portales

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Pregunta: ¿Usar Hola nueva Advanced Analytics portal o seguir usando el portal de la búsqueda de registro de hello?
Puede ver una comparación de portales de hello dos en [portales para crear y editar consultas de registros de análisis de registros de Azure](log-analytics-log-search-portals.md).  Cada uno tiene distintas ventajas para que pueda elegir Hola uno mejor para sus requisitos.  Es consultas toowrite comunes en el portal de análisis avanzado de Hola y pegarlos en otros lugares, como el Diseñador de vistas.  Infórmese sobre [emite tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) cuando lo hace.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Pregunta: ¿Hay algún cambio en la integración con Power BI?
Sí.  Una vez que se ha actualizado el área de trabajo Hola proceso de exportación de datos de análisis de registros tooPower BI ya no funcionará.  Se deshabilitarán las programaciones existentes creadas antes de actualizar.  Después de la actualización, usa Azure Log Analytics Hola misma plataforma que Application Insights y usar Hola mismo proceso tooPower de consultas de análisis de registros tooexport BI como [Hola proceso tooexport Application Insights consulta tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Problema conocido: Límite de tamaño de solicitud de Power BI
Actualmente hay un límite de tamaño de 8 MB para una consulta de análisis de registros que puede ser exportado tooPower BI.  Este límite se a aumentará próximamente.


##<a name="powershell-cmdlets"></a>Cmdlets de PowerShell

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Pregunta: Hola cmdlet de PowerShell de búsqueda de registro se actualiza una vez actualizar?
Hola [AzureRmOperationalInsightsSearchResults Get](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) aún no se ha actualizado toohello nuevo lenguaje de búsqueda.  Continuar el lenguaje de consulta heredado de toouse Hola con este cmdlet, incluso después de actualizar el área de trabajo.  Documentación actualizada estará disponible para el cmdlet de hello cuando se actualiza.


## <a name="resource-manager-templates"></a>Plantillas de Resource Manager

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Pregunta: ¿Puedo crear un área de trabajo actualizada con una plantilla de Resource Manager?
Sí.  Debe usar una versión de API de vista previa de 2017-03-15 e incluir un **características** sección en la plantilla como en el siguiente ejemplo de Hola.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Soluciones

### <a name="question-will-my-solutions-continue-toowork"></a>Pregunta: ¿Mi soluciones seguirá toowork?
Todas las soluciones continuará toowork en un área de trabajo actualizado, aunque su rendimiento mejorará si son toohello convertido nuevo lenguaje de consulta.  Existen problemas conocidos con algunas soluciones existentes que se describen en esta sección.

### <a name="known-issue-capacity-and-performance-solution"></a>Problema conocido: Solución Capacity and Performance
Algunas partes de Hola Hola [capacidad y rendimiento](log-analytics-capacity.md) vista puede estar vacía.  Un problema de toothis de corrección estará disponible pronto.

### <a name="known-issue-device-health-solution"></a>Problema conocido: Solución Estado de dispositivos
Hola [solución de estado del dispositivo](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) no recopilará datos en un área de trabajo actualizado.  Un problema de toothis de corrección estará disponible pronto.

### <a name="known-issue-application-insights-connector"></a>Problema conocido: Application Insights Connector
Las perspectivas de la [solución Application Insights Connector](log-analytics-app-insights-connector.md) no se admiten actualmente en un área de trabajo actualizada.  Un problema de toothis de corrección está actualmente en el análisis.

## <a name="upgrade-process"></a>Proceso de actualización

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Pregunta: Tengo varias áreas de trabajo. ¿Puedo actualizar todas las áreas de trabajo en hello mismo tiempo?  
No.  La actualización aplica tooa sola área de trabajo cada vez. Actualmente no hay ninguna manera de actualizar muchas áreas de trabajo a la vez. Tenga en cuenta que otros usuarios del área de trabajo de hello actualizado se verán afectadas así.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Pregunta: ¿Se modificarán los datos de los registros existentes recopilados en mi área de trabajo si la actualizo?  
No. búsquedas de área de trabajo de Hello registros datos tooyour disponibles no se ve afectada por la actualización de Hola. Las búsquedas guardadas, alertas y vistas será convertido toohello nuevo lenguaje de búsqueda automáticamente.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Pregunta: ¿Qué sucede si no actualizo mi área de trabajo?  
búsqueda de registros heredado de Hello dejará de utilizarse en hello procedentes de meses. Las áreas de trabajo que no se hayan actualizado en esa fecha se actualizarán automáticamente.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Pregunta: no eligió tooupgrade pero mi área de trabajo se ha actualizado de todos modos. ¿Qué ha ocurrido?  
Otro administrador de esta área de trabajo se ha actualizado el área de trabajo de Hola. Tenga en cuenta que todas las áreas de trabajo se actualizará automáticamente al nuevo lenguaje de hello alcance la disponibilidad general.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Pregunta: ha actualizado por error y ahora necesita toocancel y restauración de todo. ¿Qué debo hacer?  
No se preocupe.  Se crea una instantánea del área de trabajo antes de la actualización, con lo cual puede restaurarla si es necesario. Tenga en cuenta que busca, alertas o vistas que ha guardado después de la actualización de Hola se perderá aunque.  ¿toorestore su entorno de área de trabajo, siga Hola procedimiento en [puedo ir después de actualizar?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Vistas

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Pregunta: ¿Cómo puedo crear una vista con el Diseñador de vistas?
Tooupgrade anterior, podría crear una nueva vista con el Diseñador de vistas de un icono en el panel principal Hola.  Cuando se actualiza el área de trabajo, este elemento se elimina.  Puede crear una nueva vista con el Diseñador de vistas en el portal de OMS Hola haciendo clic en el botón en el menú de la izquierda Hola + Hola verde.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Problema conocido: La opción Ver todo para los gráficos de líneas de las vistas no genera un gráfico de líneas
Al hacer clic en hello *ver todas* opción final Hola de un elemento de gráfico de línea en una vista, se le presentará una tabla.  Tooupgrade anterior, se podría presentará un gráfico de líneas.  Este problema se está analizando para una posible modificación.


## <a name="next-steps"></a>Pasos siguientes

- Obtenga más información sobre [actualizar el área de trabajo toohello lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md).
