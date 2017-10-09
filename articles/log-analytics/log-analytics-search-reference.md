---
title: "referencia de búsqueda de análisis de registros aaaAzure | Documentos de Microsoft"
description: "referencia de búsqueda de análisis de registros de Hello describe el lenguaje de búsqueda de Hola y proporciona opciones de sintaxis de consulta general de Hola que puede usar al buscar datos y filtrar expresiones toohelp limitar la búsqueda."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Referencia sobre búsqueda de registros de Log Analytics

>[!NOTE]
> Este artículo describen las búsquedas de registros usando el lenguaje de consulta actual de hello en análisis de registros.  Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, debe hacer referencia demasiado[Hola referencia del lenguaje para el nuevo lenguaje de hello](https://go.microsoft.com/fwlink/?linkid=856079).

Hello siguiente sección de referencia sobre el lenguaje de búsqueda describe las opciones de sintaxis de consulta general Hola que puede usar al buscar datos y filtrar expresiones toohelp limitar la búsqueda. También se describen los comandos que puede usar la acción tootake en hello los datos recuperados.

Puede leer sobre los campos de hello devueltos en las búsquedas y las facetas de Hola que le ayudarán a averiguar más sobre categorías similares de datos, en hello [sección de referencia de campo de búsqueda y la faceta](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Sintaxis de consulta general
sintaxis de Hola para consultar general es como sigue:

```
filterExpression | command1 | command2 …
```

Hola expresión de filtro (`filterExpression`) define Hola Hola de condición "where" para la consulta. comandos de Hola aplican resultados toohello devueltos por la consulta de Hola. Varios comandos deben separarse con hello barra vertical (|).

### <a name="general-syntax-examples"></a>Ejemplos de sintaxis general
Ejemplos:

```
system
```

Esta consulta devuelve resultados que contengan la palabra Hola *system* en cualquier campo que se ha indexado para texto completo o de los términos de búsqueda.

> [!NOTE]
> No todos los campos se indexan de este modo, pero son más comunes campos textual (por ejemplo, nombres y descripciones) normalmente Hola.
>
>

```
system error
```

Esta consulta devuelve resultados que contienen palabras hello *system* y *error*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Esta consulta devuelve resultados que contienen palabras hello *system* y *error*. A continuación, ordena los resultados de Hola por hello *ManagementGroupName* campo (en orden ascendente) y, a continuación, hello *TimeGenerated* campo (en orden descendente). Toma Hola solo 10 primeros resultados.

> [!IMPORTANT]
> Hola a todos los nombres de campo y valores de hello para los campos de cadena y texto hello distinguen mayúsculas de minúsculas.
>
>

## <a name="filter-expressions"></a>Expresiones de filtro
Hola siguientes subsecciones explica las expresiones de filtro de Hola.

### <a name="string-literals"></a>Literales de cadena
Un literal de cadena es cualquier cadena que no se reconoce el analizador de hello como una palabra clave o un tipo de datos predefinido (por ejemplo, un número o fecha).

Ejemplos:

```
These all are string literals
```

Esta consulta busca los resultados que contienen las apariciones de las cinco palabras. tooperform una búsqueda de cadena compleja, incluya Hola literal de cadena de comillas. Por ejemplo:

```
"Windows Server"
```

Esto solo devuelve resultados con coincidencias exactas de *Windows Server*.

### <a name="numbers"></a>Números
Analizador de Hello admite Hola decimal sintaxis de entero y punto flotante para campos numéricos.

Ejemplos:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Fechas y horas
Cada parte de los datos de sistema de hello tiene un *TimeGenerated* que representa Hola fecha y hora originales del registro de hello. Algunos tipos de datos pueden tener más campos de fecha y hora (por ejemplo, *LastModified*).

Hola escala de tiempo **gráfico y hora** selector de análisis de registros de Azure muestra una distribución de los resultados con el tiempo (correspondiente toohello consulta actual que se ejecuta). Esto se basa en hello *TimeGenerated* campo. Campos de fecha y hora tienen un formato de cadena específico que se puede usar en consultas toorestrict Hola consulta tooa período de tiempo concreto. También puede utilizar la sintaxis toorefer toorelative intervalos de tiempo (por ejemplo, "entre hace tres días y hace dos horas").

siguiente Hola es formatos válidos de sintaxis para las fechas y horas:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


Por ejemplo:

```
TimeGenerated:2013-10-01T12:20
```

comando de Hello anterior solo devuelve los registros con un *TimeGenerated* valor de exactamente 12:20 del 1 de octubre de 2013.

Analizador de Hello también es compatible con valor de fecha y hora mnemotécnico hello, ahora. (No es probable que esto produzca ningún resultado porque los datos no pasan a través del sistema de hello tan rápido).

Estos ejemplos son bloques de creación toouse fechas relativas y absolutas. En Hola siguientes tres subsecciones, verá cómo toouse en más avanzadas de filtros, con ejemplos que utilizan intervalos de fechas relativas.

### <a name="datetime-math"></a>Operadores matemáticos Date/Time
Usar toooffset de operadores de matemáticas de fecha y hora de Hola o redondear el valor de fecha y hora de hello, mediante el uso de cálculos de fecha y hora sencillos.

Sintaxis:

```
datetime/unit
```

```
datetime[+|-]count unit
```

| Operador | Descripción |
| --- | --- |
| / |Toohello de fecha y hora se redondeará especifica la unidad. Por ejemplo, ahora / DAY redondea hello toomidnight de fecha y hora actual del programa Hola día actual. |
| + o - |Fecha y hora de desplazamientos por hello número especificado de unidades. Por ejemplo, Now+1hour desplaza Hola actual fecha/hora una hora hacia adelante. 2013-10-01T12:00-10DAYS desplaza el valor de fecha de hello 10 días. |

Puede encadenar juntos operadores matemáticos de fecha y hora de Hola. Por ejemplo:

```
NOW+1HOUR-10MONTHS/MINUTE
```

Hello tabla siguiente enumeran Hola admitida unidades de fecha y hora.

| Unidad Date/Time | Descripción |
| --- | --- |
| AÑO, AÑOS |Redondea toocurrent año o desplazamientos por hello número especificado de años. |
| MES, MESES |Redondea toocurrent mes o desplazamientos por hello número especificado de meses. |
| DÍA, DÍAS, FECHA |Día de toocurrent ciclos de mes de Hola o desplazamientos por hello número especificado de días. |
| HORA, HORAS |Hora de toocurrent ciclos o desplazamientos por hello número especificado de horas. |
| MINUTO, MINUTOS |Redondea toocurrent minute o desplazamientos por hello número especificado de minutos. |
| SEGUNDO, SEGUNDOS |Redondea toocurrent en segundo lugar, o desplaza Hola especificada número de segundos. |
| MILISEGUNDO, MILISEGUNDOS, MILI, MILIS |Los milisegundos de toocurrent ciclos o desplazamientos por hello número especificado de milisegundos. |

### <a name="field-facets"></a>Facetas de campo
Mediante el uso de facetas de campo, puede especificar la condición de búsqueda de Hola para campos específicos y sus valores exactos. Esto difiere de escribir consultas de "texto libre" para varios términos en todo el índice de Hola. Ya ha visto esta técnica en varios ejemplos anteriores. los siguientes Hola son ejemplos más complejos.

**Sintaxis**

```
field:value
```

```
field=value
```

**Descripción**

Búsquedas Hola campo valor específico de Hola. Hola valor puede ser un literal de cadena, número, o fecha y hora.

Por ejemplo:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Sintaxis**

*field&gt;value*

*field&lt;value*

*field&gt;=value*

*field&lt;=value*

*field!=value*

**Descripción**

Proporciona comparaciones.

Por ejemplo:

```
TimeGenerated>NOW+2HOURS
```

**Sintaxis**

```
field:[from..to]
```

**Descripción**

Proporciona facetas de intervalo.

Por ejemplo:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
Hola **IN** palabra clave permite tooselect desde una lista de valores. Función que use la sintaxis de hello, esto puede ser una simple lista de valores que proporcione o una lista de valores de una agregación.

Sintaxis 1:

```
field IN {value1,value2,value3,...}
```

Esta sintaxis permite tooinclude todos los valores en una lista simple.



Ejemplos:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Sintaxis 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Esta sintaxis permite toocreate una agregación. A continuación, puede incorporar lista de Hola de valores de esa agregación en otra búsqueda externa (principal) que comprueba si hay eventos con esos valores. Para ello escriba búsqueda interna Hola entre llaves e incorpore sus resultados como valores posibles de un campo de búsqueda externa hello mediante hello en operador.

Ejemplo de consulta interna: *que les faltan actualmente actualizaciones de seguridad de equipos* con hello después de consulta de agregación:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

consulta final de Hola que busca *todos los eventos de Windows para equipos que les faltan actualmente actualizaciones de seguridad* se asemeja a Hola siguiente:

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contains
Hola **Contains** palabra clave permite toofilter para los registros con un campo que contiene una cadena especificada. Esto distingue mayúsculas de minúsculas, solo funciona con campos de cadena y no puede incluir cualquier carácter de escape.

Sintaxis:

```
field:contains("string")
```

Ejemplo:

```
Type:contains("Event")
```

Esto devuelve los registros con un tipo que contiene la cadena hello "Evento". Algunos ejemplos son **Event**, **SecurityEvent** y **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Expresiones regulares
Puede especificar una condición de búsqueda para un campo con una expresión regular, mediante el uso de hello **Regex** palabra clave. Para obtener una descripción completa de sintaxis de Hola que puede usar en expresiones regulares, vea [mediante búsquedas de expresiones regulares toofilter registros de análisis de registros](log-analytics-log-searches-regex.md).

Sintaxis:

```
field:Regex("Regular Expression")
```

Ejemplo:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Operadores lógicos
consulta de Hello lenguajes admiten operadores lógicos hello (*AND*, *o*, y *no*) y sus alias de estilo C (*&&*,  *||* , y *!*, respectivamente). Puede usar paréntesis toogroup estos operadores.

Ejemplos:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

Puede omitir el operador lógico de Hola para argumentos de filtro de nivel superior de Hola. En este caso, se supone Hola operador AND.

| Expresión de filtro | Equivalente demasiado|
| --- | --- |
| error del sistema |sistema Y error |
| sistema "Windows Server" O gravedad:1 |sistema Y "Windows Server" O gravedad:1 |

### <a name="wildcarding"></a>Caracteres comodín
lenguaje de consulta de Hello admite el uso de hello ( \* ) caracteres demasiado representan uno o más caracteres de un valor en una consulta.

Ejemplo:

 Buscar todos los equipos con "SQL" en nombre de hello, como "Redmond SQL".

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> Actualmente no se pueden usar caracteres comodín entrecomillados. Por ejemplo, el mensaje de saludo `"*This text*"` considera hello (\*) utiliza como un literal (\*) caracteres.


## <a name="commands"></a>Comandos:


comandos de Hola aplican toohello resultados devueltos por la consulta de Hola. Use Hola canalización carácter (|) tooapply una toohello comando recupera resultados. Varios comandos deben separarse con hello barra vertical.

> [!NOTE]
> Nombres de los comandos pueden escribirse en mayúsculas o minúsculas, a diferencia de los nombres de campo de Hola y datos de Hola.
>
>

### <a name="sort"></a>Sort
Sintaxis:

    sort field1 asc|desc, field2 asc|desc, …

Ordena los resultados de Hola por campos concretos. Hola asc o desc sufijo toosort Hola results en orden ascendente o descendente es opcional. Si se omite, Hola *asc* supone el criterio de ordenación. Para hello **TimeGenerated** campo, *desc* se supone el criterio de ordenación, por lo que devuelve resultados más recientes de hello primero de forma predeterminada.

### <a name="toplimit"></a>Top/Limit
Sintaxis:

    top number


    limit number
Límites de Hola respuesta toohello primeros N resultados.

Ejemplo:

    Type:Alert errors detected | top 10

Devuelve Hola primeros 10 resultados coincidentes.

### <a name="skip"></a>Skip
Sintaxis:

    skip number

Omite la Hola número de resultados que se enumeran.

Ejemplo:

    Type:Alert errors detected | top 10 | skip 200

Devuelve los 10 resultados principales coincidentes empezando por el resultado 200.

### <a name="select"></a>Seleccionar
Sintaxis:

    select field1, field2, ...

Limita los campos de resultados toohello elegidos.

Ejemplo:

    Type:Alert errors detected | select Name, Severity

Límites de Hola campos de resultados devueltos demasiado*nombre* y *gravedad*.

### <a name="measure"></a>Measure
Hola *medida* comando es tooapply usa las funciones estadísticas toohello búsqueda sin procesar resultados. Esto es muy útil tooget *Agrupar por* vistas a través de los datos de Hola. Cuando se usa el comando measure de hello, búsqueda de análisis de registros muestra una tabla con resultados agregados.

**Sintaxis:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Agrega los resultados de Hola por *groupField*y calcula los valores de medida de Hola que se agregan mediante el uso de *aggregatedField*.

| Función estadística de medida | Descripción |
| --- | --- |
| *aggregateFunction* |nombre de Hola de función de agregado de hello (con distinción entre mayúsculas y minúsculas). se admite Hola siguiendo las funciones de agregado: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, percentil ## o PCT ## (## es cualquier número entre 1 y 99). |
| *aggregatedField* |campo de Hola que se está agregando. Este campo es opcional para la función de agregado COUNT de hello, pero tiene toobe un campo numérico existente para SUM, MAX, MIN, AVG, STDDEV, percentil ## o PCT ## (## es cualquier número entre 1 y 99). Hola aggregatedField también puede ser cualquiera de hello **extender** funciones admitidas. |
| *fieldAlias* |alias (opcional) Hola Hola calcula el valor agregado. Si no se especifica, el nombre del campo de hello es **AggregatedValue**. |
| *groupField* |nombre de Hola de hello campo del conjunto de resultados de Hola se agrupa por. |
| *Intervalo* |intervalo de tiempo de Hello, en formato de hello:**nnnNAME**. **nnn**es el número entero positivo de Hola. **NOMBRE** es el nombre del intervalo de saludo. Los nombres de intervalo admitidos distinguen mayúsculas de minúsculas e incluyen: MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S] y YEAR[S]. |

opción de intervalo de Hola solo puede usarse en campos de grupo de fecha y hora (como *TimeGenerated* y *TimeCreated*). Actualmente, esto no se aplica al servicio de hello, pero un campo sin fecha y hora que se pasa toohello back-end produce un error en tiempo de ejecución. Cuando se implementa la validación del esquema hello, Hola API del servicio rechaza las consultas que usan campos sin fecha y hora para la agregación de intervalo. Hola actual *medida* implementación admite la agrupación de intervalo para cualquier función de agregado.

Si se omite la cláusula BY de hello, pero se especifica un intervalo (como una segunda sintaxis), Hola *TimeGenerated* se usa de forma predeterminada.

Ejemplos:

**Ejemplo 1**

    Type:Alert | measure count() as Count by ObjectId

Grupos de Hola alertas por *ObjectID*y calcula el número de Hola de alertas para cada grupo. Hello agregado se devuelve como valor hello *recuento* campo (alias).

**Ejemplo 2**

    Type:Alert | measure count() interval 1HOUR

Grupos de Hola alertas por intervalos de 1 hora mediante el uso de hello *TimeGenerated* campo y devuelve el número de Hola de alertas en cada intervalo.

**Ejemplo 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Igual que el anterior ejemplo de Hola, pero con un alias de campo agregado (*AlertsPerHour*).

**Ejemplo 4**

    * | measure count() by TimeCreated interval 5DAY

Agrupa los resultados de hello en intervalos de 5 días mediante el uso de hello *TimeCreated* campo y devuelve el número de Hola de resultados en cada intervalo.

**Ejemplo 5**

    Type:Alert | measure max(Severity) by WorkflowName

Grupos de Hola alertas por nombre de la carga de trabajo y devuelve Hola valor máximo de gravedad de alerta para cada flujo de trabajo.

**Ejemplo 6**

    Type:Alert | measure min(Severity) by WorkflowName

Igual que el anterior ejemplo de Hola, pero con hello *min* función agregada.

**Ejemplo 7**

    Type:Perf | measure avg(CounterValue) by Computer

Grupos de rendimiento por equipo y calcula Hola promedio (avg).

**Ejemplo 8**

    Type:Perf | measure sum(CounterValue) by Computer

Igual que el ejemplo anterior de hello, pero usa *suma*.

**Ejemplo 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Igual que el ejemplo anterior de hello, pero usa *stddev*.

**Ejemplo 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Igual que el ejemplo anterior de hello, pero usa *percentile70*.

**Ejemplo 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Igual que el ejemplo anterior de hello, pero usa *pct70*. Tenga en cuenta que *PCT##* es solo un alias de la función *PERCENTILE##*.

**Ejemplo 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Agrupa rendimiento primero por equipo y, a continuación, CounterName y calcula Hola promedio (avg).

**Ejemplo 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Obtiene Hola superiores cinco flujos de trabajo con el número máximo de Hola de alertas.

**Ejemplo 14**

    * | measure countdistinct(Computer) by Type

Cuenta el número de Hola de generación de informes para cada tipo de equipos únicos.

**Ejemplo 15**

    * | measure countdistinct(Computer) Interval 1HOUR

Cuenta el número de Hola de equipos únicos reporting para cada hora.

**Ejemplo 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

Grupos de % de tiempo de procesador por equipo y devuelve el promedio de Hola para cada hora.

**Ejemplo 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

Agrupa W3CIISLog método y devuelve Hola máximo para cada 5 minutos.

**Ejemplo 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Grupos % Processor Time por equipo y devuelve Hola mínimo, promedio, percentil 75 y máximo para cada hora.

**Ejemplo 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Grupos % Processor Time primero por el equipo y, a continuación, percentil 75 instancia nombre y devuelve Hola mínimo, promedio y máximo para cada hora.

**Ejemplo 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Calcula el máximo de Hola de escrituras en disco por minuto para todos los discos en el equipo.

### <a name="where"></a>Where
Sintaxis:

```
**where** AggregatedValue>20
```

Solo puede usarse después un *medida* Hola de filtro de toofurther comando agregado da como resultado que hello *medida* ha creado.

Ejemplos:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Dedup
Sintaxis:

    Dedup FieldName

Devuelve Hola primer documento encontrado para cada valor único de hello dado campo.

Ejemplo:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

En este ejemplo se devuelve un evento (evento más reciente de hello) por Id. de evento.

### <a name="join"></a>Unión
Combinaciones Hola resultados de dos consultas tooform un único conjunto de resultados.  Admite varios tipos de combinaciones descritos en hello siga tabla.

| Tipo de combinación | Descripción |
|:--|:--|
| interna | Devuelve solo aquellos registros con un valor coincidente en ambas consultas. |
| externa | Devuelve todos los registros de ambas consultas.  |
| izquierda  | Devuelve todos los registros de la consulta izquierda y los coincidentes de la consulta derecha. |


- Combinaciones no admiten actualmente las consultas que incluyen hello **en** palabra clave, hello **medida** comando o hello **extender** comando si dirige a un campo de consulta derecha Hola.
- De momento solo se puede incluir un campo único en una combinación.
- Una búsqueda única no puede incluir más de una combinación.

**Sintaxis**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**Ejemplos**

tipos de combinaciones diferentes de hello de tooillustrate, considere la posibilidad de unirse a un tipo de datos recopilados de un registro personalizado denominado MyBackup_CL con latido de Hola para cada equipo.  Estos tipos de datos tienen Hola después de datos.

`Type = MyBackup_CL`

| TimeGenerated | Equipo | LastBackupStatus |
|:---|:---|:---|
| 4/20/2017 01:26:32.137 AM | srv01.contoso.com | Correcto |
| 4/20/2017 02:13:12.381 AM | srv02.contoso.com | Correcto |
| 4/20/2017 02:13:12.381 AM | srv03.contoso.com | Error |

`Type = Hearbeat` (Solo se muestra un subconjunto de campos)

| TimeGenerated | Equipo | ComputerIP |
|:---|:---|:---|
| 4/21/2017 12:01:34.482 PM | srv01.contoso.com | 10.10.100.1 |
| 4/21/2017 12:02:21.916 PM | srv02.contoso.com | 10.10.100.2 |
| 4/21/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>combinación interna

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Devuelve Hola siguientes registros que coincide con el campo de equipo de Hola para ambos tipos de datos.

| Equipo| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Correcto | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Latido |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | Correcto | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Latido |


#### <a name="outer-join"></a>combinación externa

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Devuelve Hola siguientes registros para ambos tipos de datos.

| Equipo| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Correcto  | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Latido |
| srv02.contoso.com | 4/20/2017 02:14:12.381 AM | Correcto  | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Latido |
| srv03.contoso.com | 4/20/2017 01:33:35.974 AM | Error  | 4/21/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 4/21/2017 12:01:47.373 PM | 10.10.100.2 | Latido |



#### <a name="left-join"></a>combinación izquierda

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Devuelve los siguientes registros de MyBackup_CL con los campos coincidentes de latido de Hola.

| Equipo| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | Correcto | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Latido |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | Correcto | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Latido |
| srv03.contoso.com | 4/20/2017 02:13:12.381 AM | Error | | | |


### <a name="extend"></a>Extend
Le permite toocreate campos de tiempo de ejecución de consultas. Tenga en cuenta que los campos de tiempo de ejecución no se puede usar con la agregación de hello medida comando tooperform.

**Ejemplo 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Muestra una puntuación de recomendación ponderada para las recomendaciones de evaluación de SQL.

**Ejemplo 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Muestra el valor del contador en kilobytes en lugar de en bytes.

**Ejemplo 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Escalas Hola valor de WireData TotalBytes, de forma que todos los resultados oscilan entre 0 y 100.

**Ejemplo 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Etiqueta los valores de contadores de rendimiento inferiores a 50 % como LOW (bajo) y el resto como HIGH (alto).

**Ejemplo 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Calcula el máximo de Hola de escrituras en disco por minuto para todos los discos en el equipo.

**Funciones admitidas**

| Función | Descripción | Ejemplos de sintaxis |
| --- | --- | --- |
| abs |Devuelve el valor de absoluto de Hola de hello especificado valor o una función. |`abs(x)` <br> `abs(-5)` |
| acos |Devuelve el arcocoseno de un valor o una función. |`acos(x)` |
| y |Devuelve un valor True si y solo si todos sus operandos evalúan tootrue. |`and(not(exists(popularity)),exists(price))` |
| asin |Devuelve el arcoseno de un valor o una función. |`asin(x)` |
| atan |Devuelve el arco tangente de un valor o una función. |`atan(x)` |
| atan2 |Devuelve el ángulo de hello resultante de la conversión de Hola de coordenadas rectangulares de hello coordenadas x e y toopolar. |`atan2(x,y)` |
| cbrt |Raíz cúbica. |`cbrt(x)` |
| ceil |Redondea tooan entero. |`ceil(x)`  <br> `ceil(5.6)` devuelve 6. |
| cos |Devuelve el coseno de un ángulo. |`cos(x)` |
| cosh |Devuelve el coseno hiperbólico de un ángulo. |`cosh(x)` |
| def |Abreviatura de forma predeterminada. Devuelve Hola valor del campo "field". Si no existe el campo de hello, devuelve el valor predeterminado de hello especificado y devuelve Hola primer valor donde: `exists()==true`. |`def(rating,5)`. Esta función def() devuelve la clasificación de hello, o si no se especifica ninguna clasificación en el documento de hello, devuelve 5. <br> `def(myfield, 1.0)`es equivalente demasiado`if(exists(myfield),myfield,1.0)`. |
| deg |Convierte radianes toodegrees. |`deg(x)` |
| div |`div(x,y)` divide x entre y. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dist |Devuelve la distancia de hello entre dos vectores, (puntos) en un espacio de n dimensiones. Toma power hello, además de dos o más, instancias de ValueSource y calcula las distancias entre dos vectores de Hola Hola. Cada elemento ValueSource debe ser un número. Debe haber un número par de instancias de ValueSource pasadas y método hello se da por supuesto que Hola primera mitad representa el primer vector de Hola y Hola segunda mitad representa el segundo vector de Hola. |`dist(2, x, y, 0, 0)`Calcula la distancia Euclidiana Hola entre (0,0) y (x, y) para cada documento. <br> `dist(1, x, y, 0, 0)`Calcula la distancia de Manhattan (taxicab) de hello entre (0,0) y (x, y) para cada documento. <br> `dist(2,,x,y,z,0,0,0)` distancia euclidiana entre (0,0,0) y (x, y, z) para cada documento.<br>`dist(1,x,y,z,e,f,g)` distancia Manhattan entre (x, y, z) y (e, f, g), donde cada letra es un nombre de campo. |
| exists |Devuelve TRUE si algún miembro del campo de hello existe. |`exists(author)`Devuelve TRUE para cualquier documento que tiene un valor en el campo de "autor" Hola.<br>`exists(query(price:5.00))` devuelve TRUE si "price" coincide con "5.00". |
| exp |El número de Euler devuelve genera toopower x. |`exp(x)` |
| floor |Redondea hacia abajo tooan entero. |`floor(x)`  <br> `floor(5.6)` devuelve 5. |
| hypo |Devuelve sqrt(sum(pow(x,2),pow(y,2))) sin desbordamiento o subdesbordamiento intermedio. |`hypo(x,y)`  <br> ` |
| if |Permite realizar consultas de funciones condicionales. En `if(test,value1,value2)`, test es o hace referencia a valor lógico tooa o una expresión que devuelve un valor lógico (TRUE o FALSE). `value1`es el valor de hello devuelto por la función hello si prueba devuelve TRUE. `value2`es el valor de hello devuelto por la función hello si prueba devuelve FALSE. Una expresión puede ser cualquier función que genera valores booleanos. También puede ser una función que devuelve valores numéricos, en cuyo caso el valor 0 se interpreta como false, o que devuelve cadenas, en cuyo caso las cadenas vacías se interpretan como false. |`if(termfreq(cat,'electronics'),popularity,42)`Esta función comprueba cada documento toosee si contiene Hola término "electronics" en el campo de hello cat. Si lo hace, Hola, a continuación, se devuelve el valor del campo de popularidad de Hola. En caso contrario, se devuelve el valor 42 Hola. |
| linear |Implementa `m*x+c`, donde m y c son constantes y x es una función arbitraria. Esto es equivalente`sum(product(m,x),c)`, pero algo más eficaz ya que se implementa como una sola función. |`linear(x,m,c) linear(x,2,4)` devuelve `2*x+4`. |
| ln |Logaritmo natural de hello devuelve del programa Hola a la función especificada. |`ln(x)` |
| log |Devuelve Hola registro base 10 de hello función especificada. |`log(x)   log(sum(x,100))` |
| map |Asigna los valores de una función de entrada x que se encuentran en min y max, ambos inclusive toohello destino especificado. Max y min de hello argumentos deben ser constantes. predeterminado y destino de argumentos de hello pueden ser constantes o funciones. Si el valor de Hola de x no se encuentra entre min y max, a continuación, se devuelve cualquier valor de Hola de x o se devuelve un valor predeterminado si se especifica como un argumento de 5. |`map(x,min,max,target) map(x,0,0,1)`Cambia cualquier valor de 0 too1. Esto puede ser útil para procesar los valores 0 predeterminados.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`Cambia cualquier valor entre 0 y 100 too1 y todos los demás valores demasiado-1.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Cambia cualquier valor entre 0 y 100 toox + 599 y todos los demás toofrequency valores del término 'solr' en el texto del campo de Hola de Hola. |
| max |Devuelve un valor numérico máximo de varias funciones anidadas o constantes, que se especifican como argumentos de Hola: `max(x,y,...)`. función max de Hello también puede ser útil para "descender" otra función o campo a alguna constante especificada.  Hola de uso `field(myfield,max)` sintaxis para seleccionar Hola valor máximo de un único campo multivalor. |`max(myfield,myotherfield,0)` |
| Min |Devuelve un valor numérico mínimo de varias funciones anidadas o constantes, que se especifican como argumentos de Hola: `min(x,y,...)`. función min de Hello también puede ser útil para proporcionar un "límite superior" en una función mediante una constante. Hola de uso `field(myfield,min)` sintaxis para seleccionar Hola valor mínimo de un único campo multivalor. |`min(myfield,myotherfield,0)` |
| mod |Calcula el módulo de Hola de función hello x por Hola y de función. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| ms |Devuelve los milisegundos de diferencia entre sus argumentos. Las fechas son relativa toohello Unix o POSIX época temporal, medianoche del 1 de enero de 1970 UTC. Los argumentos pueden ser Hola nombre de un campo TrieDateField indexado o matemáticas de fecha en función de una fecha constante o NOW. `ms()`es equivalente demasiado`ms(NOW)`, el número de milisegundos Hola. `ms(a)`Devuelve el número de Hola de milisegundos desde la época de Hola que representa el argumento de Hola. `ms(a,b)`Devuelve el número de Hola de milisegundos que b ocurre antes de a, que es `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| not |valor de Hello niega de forma lógica del programa Hola ajustado (función). |`not(exists(author))` es TRUE solo cuando `exists(author)` devuelve false. |
| o |Una disyunción lógica. |`or(value1,value2)` devuelve TRUE si value1 o value2 son true. |
| pow |Hola genera especificado toohello base especificado power. `pow(x,y)`genera x toohello potencia de y. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`Hola igual que sqrt. |
| product |Devuelve Hola producto de varios valores o funciones, que se especifican en una lista separada por comas. `mul(...)` también puede utilizarse como alias para esta función. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |Realiza una función recíproca con `recip(x,m,a,b)` mediante la implementación de `a/(m*x+b)`, donde m, a y b son constantes, y x es cualquier función arbitrariamente compleja. Cuando a y b son iguales y x>=0, esta función tiene un valor máximo de 1 que se reduce a medida que x aumenta. Aumentar el valor de Hola de una y b conjuntamente da como resultado un movimiento de hello toda función tooa más plana parte de la curva de Hola. Estas propiedades pueden convertirla en una función idónea para aumentar más documentos recientes cuando x es `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |Convierte grados tooradians. |`rad(x)` |
| rint |Toohello se redondeará al entero más próximo. |`rint(x)`  <br> `rint(5.6)` devuelve 6. |
| sin |Devuelve el seno de un ángulo. |`sin(x)` |
| sinh |Devuelve el seno hiperbólico de un ángulo. |`sinh(x)` |
| scale |Valores de las escalas de función hello x, que se encuentran entre Hola especificar valores de minTarget y maxtarget, incluido. implementación de Hello actual recorre todos de hello función valores tooobtain Hola min y max, por lo que se puede elegir escala correcta de Hola. implementación actual de Hello no puede distinguir si los documentos se han eliminado, o los documentos que no tienen ningún valor. Utiliza valores 0,0 para estos casos. Esto significa que si los valores son normalmente todos los mayores que 0,0, uno puede todavía acabar por 0,0 como Hola min toomap de valor de. En estos casos, una adecuada `map()` función podría usarse como un valor de tooa toochange 0,0 solución alternativa en el intervalo real de hello, como se muestra aquí:`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Escalas Hola valores de x, de modo que todos los valores están comprendidos entre 1 y 2, incluido. |
| sqrt |Devuelve Hola cuadrado raíz de hello especificado valor o una función. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |Calcula la distancia de hello entre dos cadenas. Usa la interfaz de StringDistance de hello Lucene corrector comprobador y admite todas las implementaciones de hello disponibles en ese paquete. También permite que las aplicaciones tooplug en sus propios recursos mediante Solr capacidades de carga. strdist toma `(string1, string2, distance measure)`. Los posibles valores para la medición de distancia son:<ul><li>jw: Jaro-Winkler</li><li>edit: distancia Levenstein o Edit</li><li>ngram: Hola NGramDistance, si se especifica, también puede pasar tamaño ngram de hello demasiado. El valor predeterminado es 2.</li><li>FQN: Nombre de una implementación de interfaz de StringDistance Hola de clase completo. Debe tener un constructor no-arg.</li></ul> |`strdist("SOLR",id,edit)` |
| sub |Devuelve x-y de `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Sum |Devuelve Hola suma de varios valores o funciones, que se especifican en una lista separada por comas. `add(...)` también puede utilizarse como alias para esta función. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Devuelve el número de Hola de veces que aparece el término de hello en el campo de Hola para ese documento. |termfreq(text,'memory') |
| tan |Devuelve la tangente de un ángulo. |`tan(x)` |
| tanh |Devuelve la tangente hiperbólica de un ángulo. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Campo de búsqueda y referencia de faceta
Si usa los datos de toofind de búsqueda de registros, los resultados muestran distintos campos y facetas. Parte de información de hello podría no aparecer muy descriptiva. Usar hello después toohelp información entender los resultados de Hola.

| Campo | Tipo de búsqueda | Descripción |
| --- | --- | --- |
| TenantId |Todo |Usar datos de toopartition. |
| TimeGenerated |Todo |Usar escala de tiempo de toodrive hello, selectores (en la búsqueda y en otras pantallas). Representa cuándo se generó la parte de Hola de datos (normalmente en el agente de hello). tiempo de Hola se expresa en formato ISO y siempre es UTC. En caso de hello de tipos que se basan en la instrumentación existente (es decir, los eventos en un registro), suele ser Hola registró esa Hola entrada/línea/entrada de registro de tiempo real. Para algunos de hello otros tipos que se producen a través de módulos de administración o en la nube de hello (por ejemplo, recomendaciones o alertas) Hola tiempo representa algo diferente. Se trata de hora de Hola se recopiló esta nueva parte de los datos con una instantánea de una configuración de algún tipo, o una recomendación o alerta se genera según en él. |
| EventId |Evento |Id. de evento en el registro de eventos de Windows hello. |
| EventLog |Evento |Registro de eventos donde se registró el evento de Hola por Windows. |
| EventLevelName |Evento |Crítico/advertencia/información/éxito. |
| EventLevel |Evento |Valor numérico para crítico/advertencia/información/éxito (use EventLevelName en su lugar para hacer más legibles y fáciles las consultas). |
| SourceSystem |Todo |Procedencia de los datos de hello (en términos de servicio de toohello en modo de adjuntar). Por ejemplo, Microsoft System Center Operations Manager y Azure Storage. |
| ObjectName |PerfHourly |Nombre del objeto de rendimiento de Windows. |
| InstanceName |PerfHourly |Nombre de instancia del contador de rendimiento de Windows. |
| CounteName |PerfHourly |Nombre del contador de rendimiento de Windows. |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nombre para mostrar del objeto de hello dirigido por una regla de recopilación de rendimiento en Operations Manager. También podría ser el nombre para mostrar del objeto de hello descubierto por visión operativa hello, o en qué Hola se generó la alerta. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nombre para mostrar del elemento primario de hello del elemento primario de hello (en una relación de hospedaje doble) del objeto de hello dirigido por una regla de recopilación de rendimiento en Operations Manager. También podría ser el nombre para mostrar del objeto de hello descubierto por visión operativa hello, o en qué Hola se generó la alerta. |
| Equipo |La mayoría de tipos |Nombre del equipo al que pertenecen los datos de Hola. |
| DeviceName |ProtectionStatus |Datos de saludo de nombre de equipo pertenecen demasiado (igual que "Equipo"). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Categoría de estado de amenaza es una representación numérica del estado de amenaza de Hola. Códigos de respuesta tooHTTP similar, clasificación de hello tiene espacios entre los números de hello (razón de que ninguna amenaza sea 150 y no 100 o 0), y dejan espacio tooadd nuevos Estados. Para un paquete acumulativo de actualizaciones de estado de amenaza y el estado de protección, la intención de hello es tooshow Hola peor estado que Hola equipo ha estado en durante el período de tiempo seleccionado de Hola. números de Hello clasifican Hola distintos Estados, por lo que puede buscar el registro de hello con mayor número de Hola. |
| ThreatStatus |ProtectionStatus |Descripción de ThreatStatus, asigna 1:1 con ThreatStatusRank. |
| TypeofProtection |ProtectionStatus |Producto antimalware detectado en el equipo de hello: ninguno, herramienta de eliminación de Malware de Microsoft, Forefront y así sucesivamente. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |Identificador de HealthService para el agente de este equipo. |
| HealthServiceId |La mayoría de tipos |Identificador de HealthService para el agente de este equipo. |
| ManagementGroupName |La mayoría de tipos |Nombre del grupo de administración para los agentes conectados a Operations Manager. De lo contrario, es nulo o está en blanco. |
| ObjectType |ConfigurationObject |El tipo (como en la clase o el "tipo" del módulo de administración de Operations Manager) para este objeto descubierto en la evaluación de la configuración de Log Analytics. |
| UpdateTitle |RequiredUpdate |Nombre de actualización de Hola que no se encuentra instalada. |
| PublishDate |RequiredUpdate |Cuándo se publicó la actualización de hello en Microsoft Update. |
| Server |RequiredUpdate |Datos de saludo de nombre de equipo pertenecen demasiado (igual que "Equipo"). |
| Producto |RequiredUpdate |Producto que Hola actualización se aplica a. |
| UpdateClassification |RequiredUpdate |Tipo de actualización (por ejemplo, el paquete acumulativo de actualizaciones o Service Pack). |
| KBID |RequiredUpdate |Id. del artículo de KB que describe este procedimiento recomendado o esta actualización. |
| WorkflowName |ConfigurationAlert |Nombre de regla de Hola o monitor que generó la alerta de Hola. |
| Severity |ConfigurationAlert |Gravedad de alerta de Hola. |
| Prioridad |ConfigurationAlert |Prioridad de alerta de Hola. |
| IsMonitorAlert |ConfigurationAlert |¿Esta alerta la ha generado un monitor (true) o una regla (false)? |
| AlertParameters |ConfigurationAlert |XML con parámetros de Hola de alerta de análisis de registros de Hola. |
| Context |ConfigurationAlert |XML con hello contexto de alerta de análisis de registros de Hola. |
| Carga de trabajo |ConfigurationAlert |Tecnología o carga de trabajo que Hola alerta hace referencia a. |
| AdvisorWorkload |Recomendación |Tecnología o carga de trabajo que Hola recomendación hace referencia a. |
| Descripción |ConfigurationAlert |Descripción de la alerta (corta). |
| DaysSinceLastUpdate |UpdateAgent |¿Cuántos días hace (tooTimeGenerated relativa de este registro) que este agente instaló cualquier actualización de Windows Server Update Service (WSUS) o Microsoft Update? |
| DaysSinceLastUpdateBucket |UpdateAgent |Según DaysSinceLastUpdate, una categorización en ciclos de cuánto tiempo hace que un equipo ha instalado por última vez una actualización de WSUS o Microsoft Update. |
| AutomaticUpdateEnabled |UpdateAgent |¿Está habilitada o deshabilitada la comprobación automática de actualizaciones en este agente? |
| AutomaticUpdateValue |UpdateAgent |¿Es la actualización automática comprobación conjunto tooautomatically descarga e instalar, solo descargar o solo la comprobación? |
| WindowsUpdateAgentVersion |UpdateAgent |Número de versión del agente de Microsoft Update Hola. |
| WSUSServer |UpdateAgent |¿Hacia qué servidor WSUS se dirige este agente de actualización? |
| OSVersion |UpdateAgent |Versión del sistema operativo de hello en el que se ejecuta este agente de actualización. |
| Nombre |Recommendation, ConfigurationObjectProperty |Título o nombre de la recomendación de Hola o nombre de propiedad de Hola de evaluación de la configuración de análisis de registros. |
| Valor |ConfigurationObjectProperty |Valor de una propiedad de evaluación de la configuración de Log Analytics. |
| KBLink |Recomendación |Artículo KB toohello de dirección URL que describe este procedimiento recomendado o actualización. |
| RecommendationStatus |Recomendación |Las recomendaciones se encuentran entre Hola pocos tipos cuyos registros obtención el índice de búsqueda toohello actualizado y no recién agregada. Este estado cambia si Hola recomendación está activa o abierta o si el análisis de registros detecta que se ha solucionado. |
| RenderedDescription |Evento |Descripción representada (texto reutilizado con parámetros rellenados) de un evento de Windows. |
| ParameterXml |Evento |XML con parámetros de hello en la sección de datos de Hola de un evento de Windows (como se muestra en el Visor de eventos). |
| EventData |Evento |XML con la sección de datos entero de Hola de un evento de Windows (como se muestra en el Visor de eventos). |
| Origen |Evento |Origen del registro de eventos que generó el evento de Hola. |
| EventCategory |Evento |Categoría de eventos de hello, directamente desde el registro de eventos de Windows hello. |
| UserName |Evento |Nombre de usuario de eventos de Windows hello (normalmente, NT AUTHORITY\LOCALSYSTEM). |
| SampleValue |PerfHourly |Valor promedio de agregación por hora de Hola de un contador de rendimiento. |
| Min |PerfHourly |Valor mínimo de intervalo por hora de saludo de un agregado por hora del contador de rendimiento. |
| max |PerfHourly |Valor máximo de intervalo por hora de saludo de un agregado por hora del contador de rendimiento. |
| Percentile95 |PerfHourly |Hola valor del percentil 95 en intervalo por hora de Hola de un agregado por hora del contador de rendimiento. |
| SampleCount |PerfHourly |Cuántas muestras del contador de rendimiento sin procesar se han usado tooproduce este cada hora de registro agregado. |
| Threat |ProtectionStatus |Nombre del malware encontrado. |
| StorageAccount |W3CIISLog |El registro de hello Azure de la cuenta de almacenamiento se leyó desde. |
| AzureDeploymentID |W3CIISLog |Id. de implementación de Azure de registro de hello del servicio de nube de Hola que pertenece. |
| Rol |W3CIISLog |Rol del registro de hello de servicio de nube de Azure de hello al que pertenece. |
| RoleInstance |W3CIISLog |Una instancia de rol de hello rol de Azure que Hola registro al que pertenece. |
| sSiteName |W3CIISLog |Sitio Web IIS que Hola registro pertenece too(metabase notation); campo s-sitename de Hello en el registro de hello original. |
| sComputerName |W3CIISLog |campo s-computername de Hello en el registro de hello original. |
| sIP |W3CIISLog |Solicitud HTTP de Hola de dirección IP de servidor que se dirigió. campo s-ip de Hello en el registro de hello original. |
| csMethod |W3CIISLog |Método HTTP (por ejemplo, GET y POST) usado por cliente hello en solicitud de hello HTTP. Hola cs-method en el registro original de Hola. |
| cIP |W3CIISLog |Solicitud HTTP de Hola de dirección IP de cliente que proviene. campo c-ip de Hello en el registro de hello original. |
| csUserAgent |W3CIISLog |Agente de usuario HTTP declarado por cliente de hello (explorador o de otro modo). Hola a cs-user-agent en el registro de hello original. |
| scStatus |W3CIISLog |Código de estado HTTP (por ejemplo, 200/403/500) devuelto por el cliente de hello server toohello. Hola cs-status en el registro de hello original. |
| TimeTaken |W3CIISLog |¿Durante cuánto tiempo (en milisegundos) que la solicitud Hola tardó toocomplete. campo timetaken de Hello en el registro de hello original. |
| csUriStem |W3CIISLog |El identificador URI relativo (sin dirección host, es decir, /buscar) que se solicitó. campo cs-uristem de Hello en el registro de hello original. |
| csUriQuery |W3CIISLog |Consulta de URI. Las consultas URI son necesarias solo para páginas dinámicas, por ejemplo, páginas ASP, por lo que este campo normalmente contiene un guión para páginas estáticas. |
| sPort |W3CIISLog |Puerto del servidor que Hola solicitud HTTP se envió demasiado (y que escucha IIS, ya que lo seleccionó). |
| csUserName |W3CIISLog |Autentica el nombre de usuario, si Hola solicitud está autenticada y no es anónima. |
| csVersion |W3CIISLog |Versión de protocolo HTTP usada en la solicitud de hello (por ejemplo, HTTP/1.1). |
| csCookie |W3CIISLog |Información de cookies. |
| csReferer |W3CIISLog |El sitio que visitó por última vez el usuario Hola. Este sitio proporciona un vínculo toohello el sitio actual. |
| csHost |W3CIISLog |Encabezado de host (por ejemplo, www.mysite.com) que se ha solicitado. |
| scSubStatus |W3CIISLog |Código de error de subestado. |
| scWin32Status |W3CIISLog |Código de estado de Windows. |
| csBytes |W3CIISLog |Bytes enviados en la solicitud de Hola desde toohello cliente-servidor de Hola. |
| csBytes |W3CIISLog |Bytes devuelven en respuesta de Hola Hola cliente de server toohello. |
| ConfigChangeType |ConfigurationChange |Tipo de cambio (por ejemplo, WindowsServices/Software). |
| ChangeCategory |ConfigurationChange |Categoría del cambio de hello (modificado/agregado/eliminado). |
| SoftwareType |ConfigurationChange |Tipo de software (actualización/aplicación). |
| SoftwareName |ConfigurationChange |Nombre del software de hello (sólo aplicable toosoftware cambios). |
| Publicador |ConfigurationChange |Proveedor que publica software hello (sólo aplicable toosoftware cambios). |
| SvcChangeType |ConfigurationChange |Tipo de cambio que se ha aplicado en un servicio de Windows (State/StartupType/Path/ServiceAccount). Esto es aplicable tooWindows sólo los cambios de servicio. |
| SvcDisplayName |ConfigurationChange |Nombre para mostrar del servicio de Hola que se cambió. |
| SvcName |ConfigurationChange |Nombre del servicio de Hola que se ha cambiado. |
| SvcState |ConfigurationChange |Nuevo estado (actual) del servicio de Hola. |
| SvcPreviousState |ConfigurationChange |Estado conocido anterior del servicio de hello (solo es aplicable si cambia el estado del servicio). |
| SvcStartupType |ConfigurationChange |Tipo de inicio del servicio. |
| SvcPreviousStartupType |ConfigurationChange |Tipo de inicio del servicio anterior (solo es aplicable si cambia el tipo de inicio del servicio). |
| SvcAccount |ConfigurationChange |Cuenta de servicio. |
| SvcPreviousAccount |ConfigurationChange |Cuenta de servicio anterior (solo es aplicable si cambia la cuenta de servicio). |
| SvcPath |ConfigurationChange |Ejecutable de toohello de ruta de acceso del servicio de Windows hello. |
| SvcPreviousPath |ConfigurationChange |Ruta de acceso anterior del ejecutable de hello (solo es aplicable si ha cambiado) de servicio de Windows hello. |
| SvcDescription |ConfigurationChange |Descripción del servicio de Hola. |
| Anterior |ConfigurationChange |Estado anterior de este software (instalado/no instalado/versión anterior). |
| Current |ConfigurationChange |Último estado de este software (instalado/no instalado/versión anterior). |

## <a name="next-steps"></a>Pasos siguientes
Para más información acerca de las búsquedas de registros:

* Familiarizarse con [búsquedas de registro](log-analytics-log-searches.md) tooview detallada información recopilada por soluciones.
* Use [campos personalizados de análisis de registros](log-analytics-custom-fields.md) tooextend búsquedas de registros.
