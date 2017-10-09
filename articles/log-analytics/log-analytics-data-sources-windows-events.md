---
title: "aaaCollect y analizar los registros de eventos de Windows en el análisis de registros de OMS | Documentos de Microsoft"
description: "Registros de eventos de Windows son uno de los orígenes de datos más comunes Hola utilizados por el análisis de registros.  Este artículo describe cómo tooconfigure colección de registros de eventos de Windows y detalles de los registros de hello crean en el repositorio de OMS Hola."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Orígenes de datos de registros de eventos de Windows en Log Analytics
Registros de eventos de Windows son uno de los más comunes de hello [orígenes de datos](log-analytics-data-sources.md) para recopilar datos con agentes de Windows, ya que muchas aplicaciones escriben toohello registro de eventos de Windows.  Puede recopilar eventos de registros estándares, como la aplicación y del sistema en suma toospecifying los registros personalizados creados por las aplicaciones necesita toomonitor.

![Eventos de Windows](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configuración de registros de eventos de Windows
Configurar registros de eventos de Windows de hello [menú datos de configuración de análisis de registro](log-analytics-data-sources.md#configuring-data-sources).

Análisis de registros solo recopila eventos de registros de eventos de Windows hello que se especifican en la configuración de Hola.  Puede agregar un registro de eventos de escribir el nombre del registro de hello hello y haciendo clic en  **+** .  Para cada registro, se recopilan sólo los eventos Hola con niveles de gravedad de hello seleccionado.  Comprobar los niveles de gravedad de Hola para registro de hello determinado que desea toocollect.  No puede proporcionar los criterios adicionales toofilter eventos.

Tal y como se escribe el nombre de Hola de un registro de eventos, análisis de registros proporciona sugerencias de nombres comunes de registro de eventos. Si desea tooadd de registro de hello no aparece en la lista de hello, puede agregarlo escribiendo en el nombre completo de hello del registro de hello. Puede encontrar el nombre completo de hello del registro de hello mediante el Visor de eventos. En el Visor de eventos, abra hello *propiedades* página para hello registro y copia Hola cadena hello *nombre completo* campo.

![Configurar eventos de Windows](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Colección de datos
Análisis de registros recopila cada evento que coincida con una gravedad seleccionada de un registro de eventos supervisado que se crea el evento de Hola.  agente de Hello registra su lugar en cada registro de eventos que recopila de.  Si el agente de Hola se queda sin conexión durante un período de tiempo, análisis de registros recopila eventos desde donde se quedó, incluso si se crearon los eventos mientras el agente de hello estaba sin conexión.  Hay un riesgo potencial para recopilar estos eventos toonot si ajusta el registro de eventos de hello con eventos sin recopilar se sobrescriben mientras se ejecuta el agente de hello está sin conexión.

>[!NOTE]
>Log Analytics no recopila eventos de auditoría creados por SQL Server del origen *MSSQLSERVER* con Id. de evento 18453 que contengan palabras clave *Classic* o *Audit Success* y la palabra clave *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Propiedades de los registros de eventos de Windows
Registros de eventos de Windows tienen un tipo de **eventos** y que tienen propiedades de hello en hello en la tabla siguiente:

| Propiedad | Descripción |
|:--- |:--- |
| Equipo |Nombre del equipo de Hola que Hola eventos se recopilaron de. |
| EventCategory |Categoría de eventos de Hola. |
| EventData |Todos los datos con formato sin procesar. |
| EventId |Número de eventos de Hola. |
| EventLevel |Gravedad del evento de hello en formato numérico. |
| EventLevelName |Gravedad del evento de hello en formato de texto. |
| EventLog |Nombre del registro de eventos de Hola que Hola eventos se recopilaron de. |
| ParameterXml |Los valores de parámetro de evento en formato XML. |
| ManagementGroupName |Nombre del grupo de administración de Hola para los agentes de System Center Operations Manager.  En el caso de los otros agentes, este valor es AOI-<workspace ID>. |
| RenderedDescription |La descripción del evento con valores de parámetro. |
| Origen |Origen del evento de Hola. |
| SourceSystem |Tipo de evento de Hola de agente se recopilaron de. <br> OpsManager: agente de Windows, ya sea una conexión directa o administrado por Operations Manager <br> Linux: todos los agentes de Linux.  <br> AzureStorage: Diagnósticos de Azure |
| TimeGenerated |Evento de Hola de fecha y hora se creó en Windows. |
| UserName |Nombre de usuario de cuenta de hello que registró el evento de Hola. |

## <a name="log-searches-with-windows-events"></a>Búsquedas de registros con eventos de Windows
Hello tabla siguiente proporciona diferentes ejemplos de búsquedas de registros que recuperar registros de eventos de Windows.

| Consultar | Descripción |
|:--- |:--- |
| Type=Event |Todos los eventos de Windows. |
| Type=Event EventLevelName=error |Todos los eventos de Windows con gravedad de error. |
| Type=Event &#124; Measure count() by Source |Contador de eventos de Windows por origen. |
| Type=Event EventLevelName=error &#124; Measure count() by Source |Contador de eventos de error de Windows por origen. |


>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.
>
>| Consultar | Descripción |
|:---|:---|
| Evento |Todos los eventos de Windows. |
| Event &#124; where EventLevelName == "error" |Todos los eventos de Windows con gravedad de error. |
| Event &#124; summarize count() by Source |Contador de eventos de Windows por origen. |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |Contador de eventos de error de Windows por origen. |


## <a name="next-steps"></a>Pasos siguientes
* Configurar análisis de registros toocollect otros [orígenes de datos](log-analytics-data-sources.md) para el análisis.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.  
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse registros de eventos de hello en campos individuales.
* Configure la [recopilación de contadores de rendimiento](log-analytics-data-sources-performance-counters.md) desde los agentes de Windows.
