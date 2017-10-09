---
title: "solución de mantenimiento de OMS aaaAgent | Documentos de Microsoft"
description: "Este artículo está previsto toohelp comprender cómo toouse esta toomonitor solución Hola estado de los agentes que informan directamente tooOMS o System Center Operations Manager."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>Solución Agent Health en OMS
solución de estado del agente de Hello en OMS le ayuda a entender, para todos los agentes de hello informar directamente de área de trabajo OMS toohello o un tooOMS conectado del grupo de administración de System Center Operations Manager, que son no responde y enviando datos operativos.  También puede mantener un seguimiento de cuántos agentes se implementan, donde se distribuyen geográficamente y realizar otra reconocimiento de toomaintain de las consultas de distribución de Hola de agentes implementados en Azure, otros entornos de nube o local.    

## <a name="prerequisites"></a>Requisitos previos
Antes de implementar esta solución, confirme que actualmente tiene compatible [agentes de Windows](../log-analytics/log-analytics-windows-agents.md) área de trabajo OMS toohello informes o informes de tooan [grupo de administración de Operations Manager](../log-analytics/log-analytics-om-agents.md) integrado con el Área de trabajo OMS.    

## <a name="solution-components"></a>Componentes de soluciones
Esta solución consta de hello después de recursos que se agregan en el área de trabajo de tooyour y agentes directamente conectados o el grupo de administración conectados de Operations Manager.

### <a name="management-packs"></a>Módulos de administración
Si el grupo de administración de System Center Operations Manager está conectado tooan área de trabajo OMS, Hola después de módulos de administración se instala en Operations Manager.  Estos módulos de administración también se instalan en equipos Windows directamente conectados después de agregar esta solución. No hay nada tooconfigure o administrará con estos módulos de administración.

* Intelligence Pack HealthAssessment Direct Channel de Microsoft System Center Advisor (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Intelligence Pack HealthAssessment Server Channel de Microsoft System Center Advisor (Microsoft.IntelligencePacks.HealthAssessmentViaServer)  

Para obtener más información sobre cómo se actualizan los módulos de administración de soluciones, consulte [tooLog de conexión de Operations Manager análisis](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Configuración
Agregar tooyour solución Hola estado del agente que se describe el área de trabajo OMS mediante el proceso de hello en [agregar soluciones](../log-analytics/log-analytics-add-solutions.md). No es necesario realizar ninguna configuración más.


## <a name="data-collection"></a>Colección de datos
### <a name="supported-agents"></a>Agentes admitidos
Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución.

| Origen conectado | Compatible | Description |
| --- | --- | --- |
| Agentes de Windows | Sí | Se recopilan eventos de latido de agentes directos de Windows.|
| Grupo de administración de System Center Operations Manager | Sí | Eventos de latidos se recopilan de agentes que informan de grupo de administración de toohello cada 60 segundos y, a continuación, reenvían tooLog análisis. Análisis de una conexión directa de tooLog de agentes de Operations Manager no es necesario. Datos de evento de latido se reenvían desde el repositorio de análisis de registros de toohello del grupo de administración de Hola.|

## <a name="using-hello-solution"></a>Uso de solución de Hola
Cuando se agrega el área de trabajo de hello solución tooyour OMS, Hola **estado del agente** mosaico se agregarán tooyour panel de OMS. Este icono muestra número total de Hola de agentes y el número de Hola de agentes que no responde en hello últimas 24 horas.<br><br> ![Icono de la solución Agent Health en el panel](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Haga clic en hello **estado del agente** icono tooopen hello **estado del agente** panel.  panel de Hello incluye columnas de hello en hello en la tabla siguiente. Cada columna muestra eventos de diez principales Hola por el número que coincide con la que han especificado criterios de la columna para hello intervalo de tiempo. Puede ejecutar una búsqueda de registros que proporciona la lista completa de hello seleccionando **ver todas** en hello derecha, abajo de cada columna, o haciendo clic en el encabezado de columna de Hola.

| Columna | Descripción |
|--------|-------------|
| Agent count over time (Número de agentes a lo largo del tiempo) | Una tendencia del número de agentes durante un período de siete días para agentes de Linux y Windows.|
| Count of unresponsive agents (Número de agentes que no responden) | Una lista de agentes que todavía no ha enviado un latido en hello las últimas 24 horas.|
| Distribution by OS Type (Distribución por tipo de sistema operativo) | Una división de cuántos agentes de Windows y Linux tiene en su entorno.|
| Distribution by Agent Version (Distribución por versión del agente) | Una partición de versiones de agente diferente de hello instaladas en su entorno y un recuento de cada uno de ellos.|
| Distribution by Agent Category (Distribución por categoría del agente) | Una partición de las diferentes categorías de Hola de agentes que se va a enviar eventos de latido: agentes directa, agentes de OpsMgr o hello servidor de administración de Operations Manager.|
| Distribution by Management Group (Distribución por grupo de administración) | Una partición de diferentes grupos de administración de SCOM hello en su entorno.|
| Geo-location of Agents (Geolocalización de los agentes) | Una partición de distintos países de Hola donde haya agentes y un recuento total del número de Hola de agentes que se hayan instalado en cada país.|
| Count of Gateways Installed (Número de puertas de enlace instaladas) | número de Hola de servidores que tienen Hola instalada de puerta de enlace de OMS y una lista de estos servidores.|

![Ejemplo de panel de la solución Agent Health](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Registros de Log Analytics
solución de Hello crea un tipo de registro en el repositorio OMS Hola.  

### <a name="heartbeat-records"></a>Registros de latidos
Se crea un registro del tipo **Heartbeat**.  Estos registros tienen propiedades de hello en hello en la tabla siguiente.  

| Propiedad | Descripción |
| --- | --- |
| Tipo | *Heartbeat*|
| Categoría | El valor es *Direct Agent*, *SCOM Agent* o *SCOM Management Server*.|
| Equipo | Nombre del equipo.|
| OSType | Sistema operativo Windows o Linux.|
| OSMajorVersion | Versión principal del sistema operativo.|
| OSMinorVersion | Versión secundaria del sistema operativo.|
| Versión | Versión del agente de OMS o de Operations Manager.|
| SCAgentChannel | El valor es *Direct* o *SCManagementServer*.|
| IsGatewayInstalled | Si está instalada la puerta de enlace de OMS, el valor es *true*; en caso contrario, es *false*.|
| ComputerIP | Dirección IP del equipo de Hola.|
| RemoteIPCountry | Ubicación geográfica donde el equipo está implementado.|
| ManagementGroupName | Nombre del grupo de administración de Operations Manager.|
| SourceComputerId | Identificador único del equipo.|
| RemoteIPLongitude | Longitud de la ubicación geográfica del equipo.|
| RemoteIPLatitude | Latitud de la ubicación geográfica del equipo.|

Cada agente de servidor de administración de Operations Manager tooan enviará dos latidos y valor de la propiedad SCAgentChannel incluirá tanto reporting **directa** y **SCManagementServer** dependiendo de lo que Orígenes de datos de análisis de registro y soluciones que haya habilitado en su suscripción de OMS. Si recuerda, datos de soluciones son envían directamente desde un administrador de operaciones de servicio web de administración servidor toohello OMS, o debido a Hola volumen de datos recopilados en el agente de hello, se envían directamente desde el servicio web de hello agente tooOMS. Eventos de latido que tienen valor hello **SCManagementServer**, hello ComputerIP valor es la dirección IP de Hola Hola del servidor de administración ya que realmente se cargan datos de hello en él.  De latidos que SCAgentChannel se establece demasiado**directa**, es Hola de dirección IP pública del agente de Hola.  

## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo
Hello tabla siguiente proporciona búsquedas de registros de ejemplo para los registros recopilados por esta solución.

| Consultar | Descripción |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Número total de agentes |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Número de agentes que no responde en hello últimas 24 horas |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Número de agentes que no responde en hello últimos 15 minutos |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Equipos en línea (Hola últimas 24 horas) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Total agentes sin conexión en los últimos 30 minutos (Hola últimas 24 horas) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Obtener una tendencia de número de agentes a lo largo del tiempo por tipo de sistema operativo|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Distribution by OS Type (Distribución por tipo de sistema operativo) |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Distribution by Agent Version (Distribución por versión del agente) |
| Type=Heartbeat&#124;measure count() by Category |Distribution by Agent Category (Distribución por categoría del agente) |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Distribution by Management Group (Distribución por grupo de administración) |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Geo-location of Agents (Geolocalización de los agentes) |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Número de puertas de enlace de OMS instaladas |


>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](../log-analytics/log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.
>
>| Consultar | Descripción |
|:---|:---|
| Heartbeat &#124; distinct Computer |Número total de agentes |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Número de agentes que no responde en hello últimas 24 horas |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Número de agentes que no responde en hello últimos 15 minutos |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Equipos en línea (Hola últimas 24 horas) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Total agentes sin conexión en los últimos 30 minutos (Hola últimas 24 horas) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Obtener una tendencia de número de agentes a lo largo del tiempo por tipo de sistema operativo|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Distribution by OS Type (Distribución por tipo de sistema operativo) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Distribution by Agent Version (Distribución por versión del agente) |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Distribution by Agent Category (Distribución por categoría del agente) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Distribution by Management Group (Distribución por grupo de administración) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Geo-location of Agents (Geolocalización de los agentes) |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Número de puertas de enlace de OMS instaladas |

## <a name="next-steps"></a>Pasos siguientes

* Obtenga información sobre [alertas en Log Analytics](../log-analytics/log-analytics-alerts.md) para más detalles sobre la generación de alertas desde Log Analytics.
