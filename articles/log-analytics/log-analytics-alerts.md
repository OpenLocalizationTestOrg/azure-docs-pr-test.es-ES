---
title: "alertas de aaaUnderstanding en análisis de registros de Azure | Documentos de Microsoft"
description: "Alertas de análisis de registros identificar información importante en el repositorio OMS y se pueden proactivamente avisarle de problemas o invocar acciones tooattempt toocorrect ellos.  Este artículo describe Hola diferentes tipos de reglas de alerta y cómo se definen."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Información sobre alertas en Log Analytics

Las alertas de Log Analytics identifican información importante en el repositorio de Log Analytics.  Este artículo proporciona detalles de reglas de la alerta de trabajo de análisis de registros y describe las diferencias de hello entre diferentes tipos de reglas de alerta.

Para hello el proceso de creación de reglas de alerta, vea Hola siguientes artículos:

- Creación de reglas de alerta mediante [Azure Portal](log-analytics-alerts-creating.md)
- Creación de reglas de alerta mediante una [plantilla de Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Creación de reglas de alerta mediante la [API de REST](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Las reglas de alertas

Las alertas se crean mediante reglas de alerta que ejecutan automáticamente búsquedas de registros a intervalos regulares.  Si los resultados de Hola Hola de búsqueda de registros coinciden con determinados criterios, a continuación, se crea un registro de alertas.  regla de Hello, a continuación, ejecutar de forma automática una o más de las acciones tooproactively recibir una notificación de alerta de Hola o invocar otro proceso.  Diferentes tipos de reglas de alerta usan una lógica diferente tooperform este análisis.

![Alertas de Log Analytics](media/log-analytics-alerts/overview.png)

Las reglas de alertas se definen mediante Hola detalles siguientes:

- **Búsqueda de registros**.  consulta de Hola que se ejecuta cada vez que se activa la regla de alerta de Hola.  registros de Hello devueltos por esta consulta es toodetermine usado si se crea una alerta.
- **Ventana de tiempo**.  Especifica el intervalo de tiempo de Hola para consulta de Hola.  Hola consulta devuelve solo los registros que se crearon dentro de este intervalo de hello hora actual.  Puede ser cualquier valor entre 5 minutos y 24 horas. Por ejemplo, si hello vez ventana se establece too60 minutos y consulta de Hola que se ejecuta a la 1:15 P.M., se devuelve solo los registros que se han creado entre 12:15 P.M. y la 1:15 PM.
- **Frecuencia**.  Especifica la frecuencia con hello se debe ejecutar consulta. Puede ser cualquier valor entre 5 minutos y 24 horas. Debe ser igual tooor menor que el período de tiempo de Hola.  Si el valor de hello es mayor que el período de tiempo de hello, a continuación, se arriesga a registros que falta.<br>Por ejemplo, considere la posibilidad de una ventana de tiempo de 30 minutos y una frecuencia de 60 minutos.  Si se ejecuta la consulta de Hola a las 1:00, devuelve registros entre la 1:00 P.M. y de 12:30.  Hola próxima vez que se ejecutaría consulta hello es 2:00 cuando devolvería registros entre la 1:30 y las 2:00.  Nunca se evaluarán los registros creados entre la 1:00 y la 1:30.
- **Umbral**.  resultados de Hola Hola de búsqueda de registros son evaluada toodetermine si se debe crear una alerta.  umbral de Hello es diferente para distintos tipos de reglas de alerta de Hola.

Cada regla de alertas de Log Analytics es de uno de los dos tipos posibles.  Cada uno de estos tipos se describe en detalle en secciones de Hola que siguen.

- **[Número de resultados](#number-of-results-alert-rules)**. Alerta única creada cuando registros número Hola devuelven por la búsqueda de registros de hello supere un número especificado.
- **[Unidades métricas](#metric-measurement-alert-rules)**.  Alerta creada para cada objeto en los resultados de Hola Hola de búsqueda de registros con valores que sobrepasan el umbral especificado.

diferencias de Hello entre los tipos de regla de alerta son los siguientes.

- **Número de resultados** regla de alerta, siempre se creará un único tiempo de alerta **métrico** regla de alerta crea una alerta para cada objeto que supera el umbral de Hola.
- **Número de resultados** las reglas de alertas crean una alerta cuando se supera el umbral de hello una sola vez. **Métrico** reglas de alerta pueden crear una alerta cuando se supera el umbral de hello un número determinado de veces en un intervalo de tiempo determinado.

## <a name="number-of-results-alert-rules"></a>Reglas de alerta para número de resultados
**Número de resultados** reglas de alerta crean una única alerta cuando el número de Hola de registros devueltos por la consulta de búsqueda de hello sobrepasan el umbral especificado de Hola.

### <a name="threshold"></a>Umbral
umbral de Hola para un **número de resultados** regla de alerta es simplemente mayor o menor que un valor determinado.  Si el número Hola de registros devueltos por la búsqueda de registros de hello cumplan este criterio, se crea una alerta.

### <a name="scenarios"></a>Escenarios

#### <a name="events"></a>Eventos
Este tipo de regla de alertas es perfecto para trabajar con eventos como, por ejemplo, registros de eventos de Windows, Syslog y registros personalizados.  Puede que desee toocreate una alerta cuando se crea un evento de error concreto, o cuando se crean varios eventos de error dentro de un período de tiempo determinado.

tooalert en un solo evento, el número de Hola de conjunto de resultados toogreater a 0 y la frecuencia de Hola y minutos de too5 de ventana de tiempo.  Consulta de Hola que ejecuta cada 5 minutos y compruebe si hay aparición de Hola de un único evento que se creó desde que se ejecutó la consulta en Hola Hola último tiempo.  Una frecuencia mayor puede retrasar el tiempo de hello entre Hola eventos que se ha recopilado y alerta de Hola que se está creando.

Algunas aplicaciones pueden registrar un error ocasional que no tiene por qué haber generado necesariamente una alerta.  Por ejemplo, aplicación hello puede vuelva a intentar el proceso de Hola que creó el evento de error de Hola y correctamente, a continuación, Hola próxima vez.  En este caso, no puede toocreate alerta de Hola a menos que se crean varios eventos en un período de tiempo determinado.  

En algunos casos, puede querer toocreate una alerta en ausencia de Hola de un evento.  Por ejemplo, un proceso puede registrar eventos regulares tooindicate que funciona correctamente.  Si no se registra uno de estos eventos dentro de un período de tiempo determinado, debe crearse una alerta.  En este caso debe establecer el umbral de hello demasiado**menores que 1**.

#### <a name="performance-alerts"></a>Alertas de rendimiento
[Los datos de rendimiento](log-analytics-data-sources-performance-counters.md) se almacena como registros de hello tooevents similar del repositorio OMS.  Si desea tooalert cuando un contador de rendimiento supera un umbral determinado, ese umbral debe incluirse en la consulta de Hola.

Por ejemplo, si deseara tooalert cuando hello procesador se ejecuta el 90%, utilizaría una consulta como Hola siguientes con el umbral de hello para la regla de alerta de hello **mayor que 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Si deseara tooalert al procesador de hello en promedio 90% para un período de tiempo determinado, utilizaría una consulta con hello [medir comando](log-analytics-search-reference.md#commands) que Hola siguiente con el umbral de hello para la regla de alerta de hello **mayor que 0 **.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Reglas de alertas para medición de métricas

>[!NOTE]
> Las reglas de alertas para unidades métricas están actualmente en versión preliminar pública.

Las reglas de alertas para **unidades métricas** crean una alerta para cada objeto de una consulta con un valor que supera un umbral especificado.  Tienen Hola siguiendo distintas diferencias con respecto a **número de resultados** reglas de alerta.

#### <a name="log-search"></a>Búsqueda de registros
Aunque puede usar cualquier consulta para un **número de resultados** regla de alerta, hay consultas de hello requisitos específicos para una regla de alerta métrico.  Debe incluir un [medir comando](log-analytics-search-reference.md#commands) toogroup resultados de hello en un campo concreto. Este comando debe incluir Hola siguientes elementos.

- **Función de agregado**.  Determina el cálculo de Hola que se lleva a cabo y, potencialmente, un campo numérico tooaggregate.  Por ejemplo, **count()** devolverá el número de Hola de registros en la consulta de hello, **avg(CounterValue)** devolverá promedio de Hola de campo de CounterValue Hola durante el intervalo de saludo.
- **Campo de grupo**.  Se crea un registro con un valor agregado para cada instancia de este campo y se puede generar una alerta para cada una.  Por ejemplo, si deseara toogenerate una alerta para cada equipo, usaría **equipo**.   
- **Intervalo**.  Define el intervalo de tiempo de hello en el cual se agregan los datos de Hola.  Por ejemplo, si especificó **5 minutos**, se crearía un registro para cada instancia del campo de grupo de hello agregada a intervalos de 5 minutos en el período de tiempo de hello especificado para la alerta de Hola.

#### <a name="threshold"></a>Umbral
umbral de Hello métrico las reglas de alerta se define por un valor agregado y un número de infracciones.  Si cualquier punto de datos de búsqueda de registros de hello supera este valor, se considera una infracción.  Si supera el número Hola de brechas en para cualquier objeto en los resultados de Hola Hola valor especificado, se crea una alerta para ese objeto.

#### <a name="example"></a>Ejemplo
Considere la posibilidad de un escenario en el que desearía tener una alerta en caso de que cualquier equipo superara el uso del procesador en un 90 % tres veces en 30 minutos.  Podría crear una regla de alerta con hello detalles siguientes.  

**Consulta:** Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer Interval 5minute<br>
**Ventana de tiempo**: 30 minutos<br>
**Frecuencia de la alerta**: 5 minutos<br>
**Valor agregado:** mayor que 90<br>
**Desencadenar alerta según:** total de infracciones mayor que 5<br>

consulta de Hello crearía un valor medio para cada equipo a intervalos de 5 minutos.  Esta consulta se ejecutaría cada 5 minutos para los datos recopilados sobre Hola 30 minutos anteriores.  A continuación se muestran datos de ejemplo para tres equipos.

![Resultados de la consulta de ejemplo](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

En este ejemplo, se crearán alertas independientes para srv02 y srv03 desde que la infracción del umbral de hello 90% 3 veces en ventana de tiempo de Hola.  Si hello **tomando como base desencadenar la alerta:** cambiaron demasiado**consecutiva** , a continuación, se crearía una alerta solo para srv03 desde que la infracción del umbral de Hola para 3 muestras consecutivas.

## <a name="alert-records"></a>Registros de alerta
Los registros de alerta creados por reglas de alerta en Log Analytics tienen un **Tipo** de **Alerta** y un **SourceSystem** de **OMS**.  Tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*OMS* |
| *Object*  | [Alertas de métrico](#metric-measurement-alert-rules) tendrá una propiedad de campo de grupo de Hola.  Por ejemplo, si la búsqueda de registros de hello agrupa por equipo, registro de alertas de hello con tienen un campo de equipo con el nombre de hello del equipo de hello como valor de Hola.
| AlertName |Nombre de alerta de Hola. |
| AlertSeverity |Nivel de gravedad de alerta de Hola. |
| LinkToSearchResults |Vincule la búsqueda de registros de análisis de tooLog que devuelve registros de Hola de consulta de Hola que creó la alerta de Hola. |
| Consultar |Texto de consulta de Hola que se ha ejecutado. |
| QueryExecutionEndTime |Final del intervalo de tiempo de Hola para consulta de Hola. |
| QueryExecutionStartTime |Inicio del intervalo de tiempo de Hola para consulta de Hola. |
| ThresholdOperator | Operador usado por la regla de alerta de Hola. |
| ThresholdValue | Valor usado por la regla de alerta de Hola. |
| TimeGenerated |Se creó la alerta de Hola de fecha y hora. |

Hay otros tipos de alerta registros creados por hello [solución de administración de alertas](log-analytics-solution-alert-management.md) y [Power BI exporta](log-analytics-powerbi.md).  Estos tienen todos un **Tipo** de **Alerta** pero se distinguen por sus valores en **SourceSystem**.


## <a name="next-steps"></a>Pasos siguientes
* Instalar hello [solución de administración de alertas](log-analytics-solution-alert-management.md) recopilan alertas de tooanalyze creado en el análisis de registros junto con las alertas de System Center Operations Manager.
* Obtenga más información sobre las [búsquedas de registros](log-analytics-log-searches.md) que pueden generar alertas.
* Complete un tutorial para [configurar un webhook](log-analytics-alerts-webhooks.md) con una regla de alerta.  
* Obtenga información acerca de cómo toowrite [runbooks en automatización de Azure](https://azure.microsoft.com/documentation/services/automation) problemas tooremediate identificados por las alertas.
