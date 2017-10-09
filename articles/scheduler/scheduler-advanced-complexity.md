---
title: aaaHow tooBuild programaciones complejos y periodicidad avanzada con el programador de Azure
description: "Cómo tooBuild complejo programa y periodicidad avanzada con el programador de Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Cómo tooBuild complejo programa y periodicidad avanzada con el programador de Azure
## <a name="overview"></a>Información general
En el corazón de Hola de un programador de Azure trabajo es hello *programación*. programación de Hello determina cuándo y cómo Hola programador ejecuta el trabajo de Hola.

El programador de Azure permite toospecify diferentes por única vez y recurrentes programaciones para un trabajo. Las programaciones *únicas* se desencadenan una vez a una hora especificadas; en efecto, son programaciones *periódicas* que se ejecutan solo una vez. Las programaciones recurrentes se activan en una frecuencia predeterminada.

Con esta flexibilidad, Programador de Azure le permite admitir una amplia variedad de escenarios empresariales:

* Limpieza de datos periódicos; por ejemplo, todos los días hay que eliminar todos los tweets de más de 3 meses.
* Archivado: por ejemplo, cada mes, inserción factura historial toobackup servicio
* Solicitudes de datos externos; por ejemplo, cada 15 minutos hay que extraer un nuevo informe meteorológico de esquí de NOAA.
* Procesamiento de imágenes – p. ej. cada día de la semana, durante las horas, use en la nube informático imágenes toocompress cargan ese día

En este artículo se describen ejemplos de trabajos que se pueden crear con Programador de Azure. Se proporcionan datos JSON de Hola que describen cada programación. Si usas hello [API de REST de Scheduler](https://msdn.microsoft.com/library/mt629143.aspx), puede utilizar este mismo JSON para [crear un trabajo de programador de Azure](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Escenarios admitidos
Hola que muchos ejemplos de este tema muestran amplitud Hola de escenarios que admite el programador de Azure. General, estos ejemplos muestran cómo toocreate programaciones para muchos patrones de comportamiento, incluidas las Hola siguiente:

* Ejecutar una vez en una determinada fecha y hora
* Ejecutar y repetir un número de veces explícitas
* Ejecutar inmediatamente y repetir
* Ejecutar y repetir cada *n* minutos, horas, días, semanas o meses a partir de un período de tiempo determinado
* Ejecutar y repetir con frecuencia semanal o mensual, pero solo en días específicos, en determinados días de la semana o en días específicos del mes
* Ejecutar y repetir varias veces en un período; por ejemplo, el último viernes y lunes de cada mes, o a las 5:15 a.m. y a las 5:15 p.m. todos los días

## <a name="dates-and-datetimes"></a>Fechas y fecha/hora
Las fechas en los trabajos del programador de Azure siguen hello [especificación ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) e incluya solo Hola fecha.

Referencias de fecha y hora en los trabajos del programador de Azure siguen hello [especificación ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) e incluir partes de fecha y hora. Se supone que una fecha y hora que no especifica un desplazamiento de UTC toobe UTC.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Uso de JSON y API de REST para crear programaciones
Hola toocreate una programación simple utilizando [API de REST de Azure Scheduler](https://msdn.microsoft.com/library/mt629143), primero [registrar la suscripción con un proveedor de recursos](https://msdn.microsoft.com/library/azure/dn790548.aspx) (nombre del proveedor de hello para el programador es  *Microsoft.Scheduler*), a continuación, [crear una colección de trabajos](https://msdn.microsoft.com/library/mt629159.aspx)y, finalmente, [crear un trabajo](https://msdn.microsoft.com/library/mt629145.aspx). Cuando se crea un trabajo, puede especificar la programación y periodicidad mediante JSON como Hola uno ha extraído a continuación:

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Información general: conceptos básicos de esquema de trabajo
Hello en la tabla siguiente proporciona una descripción general de hello elementos principales relacionados toorecurrence y la programación de un trabajo:

| **Nombre JSON** | **Descripción** |
|:--- |:--- |
| ***startTime*** |*startTime* es una fecha y hora. Para las programaciones de simples, *startTime* es la primera aparición de Hola y para las programaciones de complejas, iniciará ningún antes de trabajo de hello *startTime*. |
| ***recurrence*** |Hola *periodicidad* objeto especifica las reglas de periodicidad para el trabajo de hello como Hola periodicidad Hola se ejecutarán con. objeto de periodicidad de Hello es compatible con elementos de hello *frecuencia, intervalo, hora de finalización, recuento,* y *programación*. Si *periodicidad* se define, *frecuencia* es necesario; Hola otros elementos de *periodicidad* son opcionales. |
| ***frequency*** |Hola *frecuencia* cadena que representa la unidad de frecuencia de hello en qué Hola se repite el trabajo. Los valores admitidos son *"minute", "hour", "day", "week",* o *"month".* |
| ***interval*** |Hola *intervalo* es un entero positivo y denota el intervalo de saludo para hello *frecuencia* que determina con qué frecuencia hello trabajo se ejecutará. Por ejemplo, si *intervalo* es 3 y *frecuencia* es "semana", el trabajo de Hola se repite cada 3 semanas. Azure Scheduler admite un valor máximo de *interval* de 18 meses para la frecuencia mensual, 78 semanas para la frecuencia semanal o 548 días para la frecuencia diaria. Por hora y minuto frecuencia, intervalo de hello admitida es de 1 < = *intervalo* < = 1000. |
| ***endTime*** |Hola *endTime* cadena especifica la fecha y hora de hello más allá de qué hello no debe ejecutar el trabajo. No es válido toohave una *endTime* Hola anteriores. Si no hay ningún *endTime* o recuento se especifica, el trabajo de Hola se ejecutará infinitamente. Ambos *endTime* y *recuento* no se pueden incluir para hello mismo trabajo. |
| ***count*** |<p>Hola *recuento* es un entero positivo (mayor que cero) que especifica el número de Hola de veces que debe ejecutarse este trabajo antes de completar.</p><p>Hola *recuento* representa Hola número de veces que se ejecuta el trabajo de hello antes de que se determina como completada. Por ejemplo, para un trabajo que se ejecuta diariamente con *recuento* 5 y fecha inicial del lunes, trabajo de hello termina después de la ejecución el viernes. Si se inicia Hola fecha está en hello anterior, primera ejecución de Hola se calcula desde la hora de creación de hello.</p><p>Si no hay ningún *endTime* o *recuento* se especifica, el trabajo de Hola se ejecutará infinitamente. Ambos *endTime* y *recuento* no se pueden incluir para hello mismo trabajo.</p> |
| ***schedule*** |Un trabajo con una frecuencia especificada modifica su periodicidad según una programación periódica. *schedule* contiene modificaciones basadas en minutos, horas, días de la semana, días del mes y número de semana. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Información general: Valores predeterminados del esquema de trabajo, límites y ejemplos
Después de esta información general, tratemos cada uno de estos elementos de detalle.

| **Nombre JSON** | **Tipo de valor** | **¿Necesario?** | **Valor predeterminado** | **Valores válidos** | **Ejemplo** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |Cadena |No |None |Fechas-horas ISO-8601 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***recurrence*** |Objeto |No |None |Objeto de periodicidad |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequency*** |Cadena |Sí |None |"minute", "hour", "day", "week", "month" |<code>"frequency" : "hour"</code> |
| ***interval*** |Number |No |1 |1 too1000. |<code>"interval":10</code> |
| ***endTime*** |Cadena |No |None |Valor de fecha y hora que representa una hora futura Hola |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***count*** |Number |No |None |>= 1 |<code>"count": 5</code> |
| ***schedule*** |Objeto |No |None |Objeto de programación |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Profundización: *startTime*
siguiente Hola tabla capturas cómo *startTime* controla cómo se ejecuta un trabajo.

| **Valor de startTime** | **Sin periodicidad** | **Periodicidad. Sin programación** | **Periodicidad con programación** |
|:--- |:--- |:--- |:--- |
| **Sin hora de inicio** |Ejecutar inmediatamente una vez |Ejecutar inmediatamente una vez. Realizar las ejecuciones posteriores basándose en el cálculo del último tiempo de ejecución. |<p>Ejecutar inmediatamente una vez</p><p>Realizar las sucesivas ejecuciones según la programación de periodicidad</p> |
| **Hora de inicio en el pasado** |Ejecutar inmediatamente una vez |<p>Calcular primero la hora de futuras ejecuciones después de la hora de inicio y ejecutarlas a esa hora</p><p>Realizar las sucesivas ejecuciones basándose en el cálculo de la última hora de ejecución</p><p>Consulte el ejemplo que sigue a esta tabla para obtener una explicación más detallada.</p> |<p>Trabajo inicia *no antes que* Hola especifica la hora de inicio. primera aparición de Hola se basa en programación de hello calculado a partir de la hora de inicio de Hola</p><p>Realizar las sucesivas ejecuciones según la programación de periodicidad</p> |
| **Hora de inicio en el futuro o en el presente** |Ejecutar una vez a la hora de inicio especificada |<p>Ejecutar una vez a la hora de inicio especificada</p><p>Realizar las ejecuciones posteriores basándose en el cálculo del último tiempo de ejecución.</p> |<p>Trabajo inicia *no antes que* Hola especifica la hora de inicio. primera aparición de Hola se basa en programación de hello calculado a partir de la hora de inicio de Hola</p><p>Realizar las sucesivas ejecuciones según la programación de periodicidad</p> |

Veamos un ejemplo de lo que sucede en *startTime* en hello anterior, con *periodicidad* pero no *programación*.  Suponga que Hola hora actual es 2015-04-08 13:00, *startTime* es 2015-04-07 14:00, y *periodicidad* es cada 2 días (definida con *frecuencia*: día y *intervalo*: 2.) Tenga en cuenta que hello *startTime* es Hola anteriores y se produce antes de hello hora actual

En estas condiciones, Hola *primera ejecución* será 2015-04-09 a las 14:00\. motor de programador de Hello calcula incidencias de ejecución de la hora de inicio de Hola.  Todas las instancias en hello anterior se descartan. motor de Hello usa instancia siguiente de Hola que tiene lugar en hello futuras.  Por lo que en este caso, *startTime* es 2015-04-07 a las 2:00 p.m., por lo que hello siguiente instancia es 2 días a partir de ese momento, que es 2015-04-09 a las 2:00 p.m..

Tenga en cuenta que la primera ejecución de hello sería Hola mismo incluso si Hola startTime 2015-04-05 14:00 o 14:00\ 2015-04-01. Tras la primera ejecución hello, las ejecuciones posteriores se calculan con hello programado: por lo que estaría en 2015-04-11 a las 2:00 p.m., a continuación, 2015-04-13 a las 2:00 p.m., a continuación, 2015-04-15 a las 2:00 p.m., etcetera.

Por último, cuando un trabajo tiene una programación, si horas o minutos no están establecidos en la programación de hello, que horas de toohello predeterminado y/o los minutos de la primera ejecución hello, respectivamente.

## <a name="deep-dive-schedule"></a>Profundización: *schedule*
Por un lado, un *programación* puede *límite* Hola número de ejecuciones de trabajos.  Por ejemplo, si un trabajo con una frecuencia de "mes" tiene un *programación* que se ejecuta en único día 31, se ejecuta el trabajo de hello en solo esos meses que tengan un 31<sup>st</sup> día.

Hola en otra parte, un *programación* también puede *expanda* Hola número de ejecuciones de trabajos. Por ejemplo, si un trabajo con una frecuencia de "mes" tiene un *programación* que se ejecuta en los días del mes 1 y 2, el trabajo de Hola se ejecuta en hello 1<sup>st</sup> y 2<sup>nd</sup> días del mes de hello en lugar de una sola vez un mes.

Si se especifican varios elementos de programación, orden de Hola de evaluación es de hello mayor toosmallest: número de semana, mes, día, día de la semana, hora y minuto.

Hello tabla siguiente se describen *programación* elementos en detalle.

| **Nombre JSON** | **Descripción** | **Valores válidos** |
|:--- |:--- |:--- |
| **minutes** |Minutos de hora de hello en qué Hola se ejecutará el trabajo |<ul><li>Entero o</li><li>Matriz de enteros</li></ul> |
| **hours** |Horas del día de hello en qué Hola se ejecutará el trabajo |<ul><li>Entero o</li><li>Matriz de enteros</li></ul> |
| **weekDays** |Días de trabajo de hello semana Hola se ejecutarán. Solo se puede especificar con una frecuencia semanal. |<ul><li>Lunes, martes, miércoles, jueves, viernes, sábado o domingo</li><li>Matriz de cualquiera de Hola por encima de valores (tamaño de la matriz max 7)</li></ul>*No* distingue mayúsculas de minúsculas |
| **monthlyOccurrences** |Determina los días de trabajo de hello mes Hola se ejecutará. Solo se puede especificar con una frecuencia mensual. |<ul><li>Matriz de objetos de monthlyOccurence:</li></ul> <pre>{ "day": *day*,<br />  "occurrence":*occurrence*<br />}</pre><p> *día* es día Hola de trabajo de hello semana Hola se ejecutará, por ejemplo, {domingo} es los domingos del mes de Hola. Necesario.</p><p>La ocurrencia es *aparición* del día de Hola durante el mes de hello, por ejemplo, {domingo, -1} se Hola último domingo del mes de Hola. Opcional.</p> |
| **monthDays** |Día de trabajo de hello mes Hola se ejecutará. Solo se puede especificar con una frecuencia mensual. |<ul><li>Cualquier valor < = -1 y > = -31.</li><li>Cualquier valor > = 1 y < = 31.</li><li>Una matriz de valores por encima</li></ul> |

## <a name="examples-recurrence-schedules"></a>Ejemplos: Programaciones de periodicidad
siguiente Hola es numerosos ejemplos de programaciones de periodicidad: centrándose en el objeto de programación de Hola y sus elementos secundarios.

Hello programaciones por debajo de todos supone que hello *intervalo* se establece too1\. Asimismo, uno debe asumir frecuencia correcta de hello en acuerdo toowhat está en hello *programación* – p. ej., uno no se usan una frecuencia de "day" y tiene una modificación de "días mes para" en programación de Hola. Estas restricciones se han descrito anteriormente.

| **Ejemplo** | **Descripción** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |Se ejecuta a las 5 a.m. cada día. El programador de Azure coincide con cada valor en "horas" con cada valor en "minutes", uno por uno, toocreate una lista de todos los tiempos de hello en qué Hola trabajo es toobe de ejecución. |
| <code>{"minutes":[15], "hours":[5]}</code> |Se ejecuta a las 5:15 a.m. cada día. |
| <code>{"minutes":[15], "hours":[5,17]}</code> |Se ejecuta a las 5:15 a.m. y 5:15 p.m. todos los días. |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |Se ejecuta a las 5:15 a.m., 5:45 a.m., 5:15 p.m. y a las 5:45 p.m. cada día. |
| <code>{"minutes":[0,15,30,45]}</code> |Se ejecuta cada 15 minutos. |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Se ejecuta cada hora. Este trabajo se ejecuta cada hora. minuto de Hola se controla mediante hello *startTime*, si se especifica uno, o si no se especifica ninguno, por hora de creación de hello. Por ejemplo, si Hola hora de inicio u hora de creación (lo que se aplica) es 12:25 P.M., trabajo Hola se ejecutarán a 00:25, 25:01, 02:25,..., 23:25. Hola programación es equivalente toohaving un trabajo con *frecuencia* de "hora", una *intervalo* 1 y n *programación*. Hello diferencia es que esta programación se podía usar con diferentes *frecuencia* y *intervalo* toocreate otro trabajos demasiado. Por ejemplo, si hello *frecuencia* fuera "mes", programación de hello ejecutaría una sola vez en un mes en lugar de todos los días si *frecuencia* estaban "día" |
| <code>{minutes:[0]}</code> |Ejecute cada hora en hora Hola. Este trabajo también ejecuta cada hora, pero en hora hello (por ejemplo, 12 A.M., 1 A.M., 2 AM, etcetera.) Esto es equivalente tooa trabajo con una frecuencia de "hora", una hora de inicio con cero minutos y ninguna programación frecuencia Hola vería "day", pero si la frecuencia de hello fuera "semana" o "mes", programación de hello ejecutaría solo un día, una semana o un día de un mes, respectivamente. |
| <code>{"minutes":[15]}</code> |Se ejecuta a «y cuarto» cada hora. Se ejecuta cada hora, comenzando en 00:15 a.m., 1:15 a.m., 2:15 a.m., etc. y terminando en 10:15 p.m. y las 11:15 p.m. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |Se ejecuta a las 5 p.m. los sábados cada semana. |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Se ejecuta a las 5 p.m. el lunes, el miércoles y el viernes de cada semana, |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Se ejecuta a las 5:15 p.m. y las 5:45 p.m. el lunes, el miércoles y el viernes cada semana. |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Se ejecuta a las 5 a.m. y a las 5 p.m. el lunes, el miércoles y el viernes de cada semana. |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Se ejecuta a las 5:15 a.m., 5:45 a.m., 5:15 p.m. y las 5:45 p.m. el lunes, el miércoles y el viernes cada semana |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Se ejecuta cada 15 minutos los días laborables. |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Se ejecuta cada 15 minutos los días laborables entre las 9 a.m. y las 4:45 p.m. |
| <code>{"weekDays":["sunday"]}</code> |Se ejecuta los domingos a la hora de inicio. |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |Se ejecuta los martes y los jueves a la hora de inicio. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |Hola de ejecución a las 6: 00 en 28 días de cada mes (con frecuencia del mes) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Ejecute a las 6 A.M. en el último día del mes de Hola Hola. Si desea que un trabajo en hello toorun último día del mes, utilice -1 en lugar de día 28, 29, 30 o 31. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |Ejecute a las 6 A.M. en hello primero y último día de cada mes |
| <code>{monthDays":[1,-1]}</code> |Ejecutar en hello primero y último día de cada mes en la hora de inicio |
| <code>{monthDays":[1,14]}</code> |Ejecutar en hello primero y decimocuarto día de cada mes en la hora de inicio |
| <code>{monthDays":[2]}</code> |Ejecutar en segundo día del mes a la hora de inicio de Hola Hola |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |Se ejecuta el primer viernes de cada mes a las 5 a.m. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: Se ejecuta el primer viernes de cada mes a la hora de inicio. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Se ejecuta el tercer viernes desde el final del mes, cada mes, a la hora de inicio. |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Se ejecuta el primer y último viernes de cada mes a las 5:15 a.m. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Se ejecuta el primer y último viernes de cada mes a la hora de inicio. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Se ejecuta el quinto viernes de cada mes a la hora de inicio. Si no hay ningún viernes quinto en un mes, esta no se ejecuta, ya que es toorun programada en viernes sólo quinto. Podría considerar el uso de -1 en lugar de 5 aparición de Hola si desea que toorun Hola trabajo en hello producen último viernes del mes de Hola. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Ejecutar cada 15 minutos en el último viernes del mes de Hola |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |Ejecute a las 5:15 A.M., 5:45 A.M., 5:15 P.M. y las 5:45 PM en Hola 3rd miércoles de cada mes |

## <a name="see-also"></a>Otras referencias
 [¿Qué es Programador?](scheduler-intro.md)

 [Conceptos, terminología y jerarquía de entidades de Programador de Azure](scheduler-concepts-terms.md)

 [Empezar a usar a Scheduler en hello portal de Azure](scheduler-get-started-portal.md)

 [Planes y facturación en Programador de Azure](scheduler-plans-billing.md)

 [Referencia de API de REST de Programador de Azure](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell de Programador de Azure](scheduler-powershell-reference.md)

 [Alta disponibilidad y confiabilidad de Programador de Azure](scheduler-high-availability-reliability.md)

 [Límites, valores predeterminados y códigos de error de Programador de Azure](scheduler-limits-defaults-errors.md)

 [Autenticación de salida de Programador de Azure](scheduler-outbound-authentication.md)

