---
title: "hoja de referencia de lenguaje de consulta de análisis de registros de aaaAzure | Documentos de Microsoft"
description: "Este artículo proporciona asistencia en transición toohello nuevo lenguaje de consulta para análisis de registros si ya está familiarizado con lenguaje heredado Hola."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Transición de lenguaje de consultas nuevo tooAzure análisis de registros

> [!NOTE]
> Puede obtener más información acerca de hello análisis de registros nuevo lenguaje de consulta y obtener Hola procedimiento tooupgrade el área de trabajo en la actualización de su [búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).

Este artículo proporciona asistencia en transición toohello nuevo lenguaje de consulta para análisis de registros si ya está familiarizado con lenguaje heredado Hola.

## <a name="language-converter"></a>Convertidor de lenguaje

Si está familiarizado con el lenguaje de consulta de análisis de registros heredado hello, hello toocreate Hola misma consulta en el nuevo lenguaje de Hola de manera más fácil es toouse hello convertidor de idioma que está instalado en el portal de la búsqueda de registro de hello cuando se convierte el área de trabajo.  Uso de convertidor de hello es tan sencillo como escribir en una consulta en el cuadro de texto superior Hola heredada y, a continuación, haga clic en **convertir**.  Puede haga clic en la consulta hello toorun botón de búsqueda de Hola o copiar y pegar toouse en otro lugar.

![Convertidor de lenguaje](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Hoja de referencia rápida

Hello tabla siguiente proporciona una comparación entre una gran variedad de consultas comunes tooequivalent comandos entre el lenguaje de consulta nuevos y antiguos de hello en análisis de registros de Azure.

| Descripción | Heredado | new |
|:--|:--|:--|
| Buscar en todas las tablas      | error | buscar "error" (no distingue mayúsculas de minúsculas) |
| Selección de datos de una tabla | Type=Event |  Evento |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| Comparación de cadenas      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Event &#124; where Computer contains "contoso" (no distingue mayúsculas de minúsculas)<br>Event &#124; where Computer contains_cs "Contoso" (distingue mayúsculas de minúsculas) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| Comparación de fechas        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| Comparación de valores booleanos     | Type=Heartbeat IsGatewayInstalled=false  | Latido | where IsGatewayInstalled == false |
| Sort                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event \| sort by Computer asc, EventLog desc, EventLevelName asc |
| Distinct               | Type=Event &#124; dedup Computer \| select Computer | Event &#124; summarize by Computer, EventLog |
| Extensión de columnas         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" \| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| Agregación            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| Agregación sin límite | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| Unión                  | Type=Event or Type=Syslog | union Event, Syslog |
| Unión                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Pasos siguientes
- Desproteger un [tutorial sobre cómo escribir consultas](https://go.microsoft.com/fwlink/?linkid=856078) utilizando Hola nuevo lenguaje de consulta.
- Consulte toohello [referencia del lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856079) para obtener más información sobre todos los comandos, operadores y funciones para el nuevo lenguaje de consulta Hola.  
