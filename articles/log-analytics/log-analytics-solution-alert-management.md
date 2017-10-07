---
title: "solución de administración de Operations Management Suite (OMS) aaaAlert | Documentos de Microsoft"
description: "Hola solución de administración de alertas en el análisis de registros le ayuda a analizar todas las alertas de hello en su entorno.  En suma tooconsolidating las alertas generadas dentro de OMS, importa las alertas de los grupos de administración de System Center Operations Manager conectados en análisis de registros."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Solución de administración de alertas de Operations Management Suite (OMS)

![Icono Administración de alertas](media/log-analytics-solution-alert-management/icon.png)

solución de administración de alertas de Hello le ayuda a analizar todas las alertas de hello en el repositorio de análisis de registros.  Estas alertas pueden proceder de diversos orígenes, incluidos los [creados por Log Analytics ](log-analytics-alerts.md) o los [importados de Nagios o Zabbix](log-analytics-linux-agents.md).  Hello solución también importa las alertas desde cualquier [grupos de administración de System Center Operations Manager conectados](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Requisitos previos
solución de Hello funciona con todos los registros en el repositorio de análisis de registros de hello con un tipo de **alerta**, por lo que debe realizar cualquier configuración es necesario toocollect estos registros.

- Para las alertas de análisis de registros, [crear reglas de alerta](log-analytics-alerts.md) registros de alerta de toocreate directamente en el repositorio de Hola.
- Para las alertas de Nagios y Zabbix, [configurar esos servidores](log-analytics-linux-agents.md) toosend alertas tooLog análisis.
- Para las alertas de System Center Operations Manager, [conectar su área de trabajo de análisis de registros de Operations Manager management grupo tooyour](log-analytics-om-agents.md).  Las alertas creadas en System Center Operations Manager se importan en Log Analytics.  

## <a name="configuration"></a>Configuración
Agregar tooyour de solución de administración de alertas de hello área de trabajo OMS mediante el proceso de Hola se describe en [agregar soluciones](log-analytics-add-solutions.md).  No es necesario realizar ninguna configuración más.

## <a name="management-packs"></a>Módulos de administración
Si el grupo de administración de System Center Operations Manager está conectado tooyour área de trabajo OMS, Hola después de módulos de administración se instala en System Center Operations Manager cuando se agrega esta solución.  No hay ninguna configuración ni mantenimiento Hola de módulos de administración necesarios.  

* Administración de alertas de Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Para obtener más información sobre cómo se actualizan los módulos de administración de soluciones, consulte [tooLog de conexión de Operations Manager análisis](log-analytics-om-agents.md).

## <a name="data-collection"></a>Colección de datos
### <a name="agents"></a>Agentes
Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución.

| Origen conectado | Soporte técnico | Descripción |
|:--- |:--- |:--- |
| [Agentes de Windows](log-analytics-windows-agents.md) | No |Los agentes directos de Windows no generan alertas.  Se pueden crear alertas de Log Analytics de eventos y datos de rendimiento recopilados desde agentes de Windows. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No |Los agentes directos de Linux no generan alertas.  Se pueden crear alertas de Log Analytics de eventos y datos de rendimiento recopilados desde agentes de Linux.  Alertas de Nagios y Zabbix se recopilan de los servidores que requieren el agente Linux de Hola. |
| [Grupo de administración de System Center Operations](log-analytics-om-agents.md) |Sí |Las alertas generadas en los agentes de Operations Manager se entregan a toohello grupo de administración y, a continuación, reenvía tooLog análisis.<br><br>Análisis de una conexión directa de tooLog de agentes de Operations Manager no es necesario. Datos de alerta se reenvían desde el repositorio de análisis de registros de toohello del grupo de administración de Hola. |


### <a name="collection-frequency"></a>Frecuencia de recopilación
- Registros de alerta son soluciones toohello disponible tan pronto como se almacenan en el repositorio de Hola.
- Datos de alertas se envían desde tooLog de grupo de administración de Operations Manager de hello análisis cada tres minutos.  

## <a name="using-hello-solution"></a>Uso de solución de Hola
Cuando se agrega el área de trabajo OMS tooyour de solución de administración de alertas de hello, Hola **administración de alertas** es agregar el icono de panel de OMS tooyour.  Este icono muestra un recuento y una representación gráfica del número de Hola de alertas activas que se generaron en hello últimas 24 horas.  Este intervalo de tiempo no se puede cambiar.

![Icono Administración de alertas](media/log-analytics-solution-alert-management/tile.png)

Haga clic en hello **administración de alertas** icono tooopen hello **administración de alertas** panel.  panel de Hello incluye columnas de hello en hello en la tabla siguiente.  Cada columna muestra hello 10 alertas principales por recuento de coincidencia que han especificado criterios de la columna para hello intervalo de ámbito y la hora.  Puede ejecutar una búsqueda de registros que proporciona la lista completa de hello haciendo clic en **ver todas** en parte inferior de la columna de Hola o haciendo clic en el encabezado de columna de Hola de Hola.

| Columna | Descripción |
|:--- |:--- |
| Alertas críticas |Todas las alertas con una gravedad crítica agrupadas por nombre de alerta.  Haga clic en un nombre de la alerta toorun una búsqueda de registros devuelve todos los registros de esa alerta. |
| Alertas de advertencia |Todas las alertas con una gravedad de advertencia agrupadas por nombre de alerta.  Haga clic en un nombre de la alerta toorun una búsqueda de registros devuelve todos los registros de esa alerta. |
| Alertas de SCOM activas |Todas las alertas procedentes de Operations Manager con cualquier estado distinto de *cerrado* agrupados por origen de esa alerta Hola generado. |
| Todas las alertas activas |Todas las alertas con cualquier gravedad agrupadas por nombre de alerta. Solo incluye las alertas de Operations Manager con cualquier estado distinto de *Cerrado*. |

Si se desplaza toohello derecha, panel de hello muestra varias consultas comunes que puede hacer clic en tooperform una [búsqueda de registros](log-analytics-log-searches.md) para datos de alertas.

![Panel Administración de alertas](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Registros de Log Analytics
solución de administración de alertas de Hello analiza todos los registros con un tipo de **alerta**.  Solución de hello directamente no recopila alertas creados por el análisis de registros o recopilado de Nagios o Zabbix.

solución de Hello importar alertas de System Center Operations Manager y crea un registro correspondiente para cada uno con un tipo de **alerta** y un SourceSystem de **OpsManager**.  Estos registros tienen propiedades de hello en hello en la tabla siguiente:  

| Propiedad | Descripción |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*OpsManager* |
| AlertContext |Detalles del elemento de datos de Hola que causó hello toobe alerta generada en formato XML. |
| AlertDescription |Descripción detallada de alerta de Hola. |
| AlertId |GUID de alerta de Hola. |
| AlertName |Nombre de alerta de Hola. |
| AlertPriority |Nivel de prioridad de alerta de Hola. |
| AlertSeverity |Nivel de gravedad de alerta de Hola. |
| AlertState |Estado más reciente de resolución de alerta de Hola. |
| LastModifiedBy |Nombre del usuario de Hola que modificó por última vez alerta Hola. |
| ManagementGroupName |Nombre del grupo de administración de Hola donde se generó la alerta de Hola. |
| RepeatCount |Número de veces Hola se generó la misma alerta para hello que mismo objeto supervisado desde el que se va a resolver. |
| ResolvedBy |Nombre del usuario de Hola que Hola alerta resuelta. Está vacío si la alerta de hello aún no se ha resuelto. |
| SourceDisplayName |Nombre de objeto que generó la alerta de Hola de supervisión de hello para mostrar. |
| SourceFullName |Nombre completo de hello supervisión de un objeto que generó la alerta de Hola. |
| TicketId |Id. de vale para la alerta de hello si el entorno de System Center Operations Manager de hello está integrado con un proceso para asignar vales para las alertas.  Vacío si no se asigna ningún vale. |
| TimeGenerated |Fecha y hora en que Hola alerta creada. |
| TimeLastModified |Fecha y hora en que Hola alerta se cambió por última vez. |
| TimeRaised |Fecha y hora en que Hola alerta generó un error. |
| TimeResolved |Fecha y hora en que Hola alerta se resolvió. Está vacío si la alerta de hello aún no se ha resuelto. |

## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo
Hello tabla siguiente proporciona búsquedas de registros de ejemplo para los registros de alerta recopilados por esta solución: 

| Consultar | Descripción |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |Alertas críticas generadas en hello las últimas 24 horas |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |Alertas de advertencia generadas en hello las últimas 24 horas |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Orígenes con alertas activas generadas en hello las últimas 24 horas |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |Alertas críticas generadas en hello las últimas 24 horas que siguen estando activas |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |Alertas generadas en hello las últimas 24 horas que ahora están cerradas |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Alertas generadas en hello último día agrupadas por su gravedad |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Alertas generadas en hello último día ordenadas por su valor de número de repeticiones |


>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola anterior consultas cambiaría toohello siguiente:
>
>| Consultar | Descripción |
|:---|:---|
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) |Alertas críticas generadas en hello las últimas 24 horas |
| Alert &#124; where AlertSeverity == "warning" and TimeRaised > ago(24h) |Alertas de advertencia generadas en hello las últimas 24 horas |
| Alert &#124; where SourceSystem == "OpsManager" and AlertState != "Closed" and TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |Orígenes con alertas activas generadas en hello las últimas 24 horas |
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) and AlertState != "Closed" |Alertas críticas generadas en hello las últimas 24 horas que siguen estando activas |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(24h) and AlertState == "Closed" |Alertas generadas en hello las últimas 24 horas que ahora están cerradas |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Alertas generadas en hello último día agrupadas por su gravedad |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; sort by RepeatCount desc |Alertas generadas en hello último día ordenadas por su valor de número de repeticiones |


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información sobre [alertas en Log Analytics](log-analytics-alerts.md) para más detalles sobre la generación de alertas desde Log Analytics.
