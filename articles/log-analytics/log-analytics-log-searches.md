---
title: "datos de aaaFind con búsquedas de registros de análisis de registros de Azure | Documentos de Microsoft"
description: "Búsquedas de registros permiten toocombine y correlacionan datos de varios orígenes en el entorno del equipo."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Descripción de las búsquedas de registros en Log Analytics

>[!NOTE]
> Este artículo describen las búsquedas de registros usando el lenguaje de consulta actual de hello en análisis de registros.  Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, debe hacer referencia demasiado[busca en el registro de descripción en análisis de registros (nuevo)](log-analytics-log-search-new.md).


Núcleo de Hola de análisis de registros es característica de búsqueda de registros de Hola que permite toocombine y correlacionar datos de varios orígenes en el entorno del equipo. Las soluciones también se basan en toobring de búsqueda de registro se métricas dinamizadas en torno a un área problemática concreta.

En la página de búsqueda de hello, puede crear una consulta y, a continuación, al realizar una búsqueda, puede filtrar los resultados de hello mediante el uso de controles de faceta. También puede crear consultas avanzadas tootransform, filtrar e informar sobre sus resultados.

En la mayoría de las páginas de soluciones aparecen consultas de búsqueda comunes. A lo largo de la consola de OMS de hello, puede hacer clic iconos o profundizar en los elementos de tooother tooview detalles sobre el elemento de hello mediante la búsqueda de registro.

En este tutorial, usaremos ejemplos toocover todos los aspectos básicos de hello cuando se utiliza la búsqueda de registros.

Se comenzaremos con ejemplos sencillos y prácticos y luego construiremos sobre ellos para que se pueda comprender los casos de uso prácticos sobre cómo visión de toouse Hola sintaxis tooextract Hola desea partir de los datos de Hola.

Cuando se haya familiarizado con las técnicas de búsqueda, puede revisar hello [referencia de búsqueda de registro de análisis de registros](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Uso de filtros básicos
Hello lo primero que tooknow es que Hola primera parte de una consulta de búsqueda, antes de cualquier "|" carácter de barra vertical, es siempre un *filtro*. Se puede considerar como una cláusula WHERE de TSQL--en determina *qué* subconjunto de datos toopull fuera del almacén de datos OMS Hola. Buscar en el almacén de datos de hello es en gran medida sobre la especificación de las características de Hola de datos de Hola que desea tooextract, por lo que es natural que una consulta comience con hello cláusula WHERE.

Hello filtros más básicos que puede usar son *palabras clave*, como 'error' o "tiempo de espera" o un nombre de equipo. Estos tipos de consultas sencillas generalmente devuelven diversas formas de datos dentro de hello mismo conjunto de resultados. Esto es porque el análisis de registro tiene diferentes *tipos* de datos en el sistema de Hola.

### <a name="tooconduct-a-simple-search"></a>tooconduct una búsqueda simple
1. En el portal de OMS de hello, haga clic en **búsqueda de registros**.  
    ![icono de búsqueda](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. En el campo de consulta de hello, escriba `error` y, a continuación, haga clic en **búsqueda**.  
    ![error de búsqueda](./media/log-analytics-log-searches/oms-search-error.png)  
    Por ejemplo, la consulta de Hola para `error` en hello siguiente imagen devolvió 100 000 **eventos** registros (recopilados por la administración de registros), 18 **ConfigurationAlert** (generados por la configuración de registros Evaluación) y 12 **ConfigurationChange** registros (capturados por seguimiento de cambios de hello).   
    ![resultados de la búsqueda](./media/log-analytics-log-searches/oms-search-results01.png)  

Estos filtros no son en realidad clases o tipos de objeto. *Tipo* es una etiqueta o una propiedad o una cadena/nombre/categoría, que está adjunta tooa parte de los datos. Algunos documentos Hola sistema están etiquetados como **Type: ConfigurationAlert** y algunas se etiquetan como **tipo: rendimiento**, o **Type: Event**, y así sucesivamente. Cada resultado de búsqueda, documento, registro o entrada muestra todas las propiedades sin procesar de Hola y sus valores para cada una de estas partes de los datos, y se puede usar esos toospecify de nombres de campo de filtro de hello cuando desee tooretrieve sólo los registros de Hola donde hello campo tiene que da valor.

*Type* es simplemente un campo que todos los registros tienen, no es diferente de ningún otro campo. Esto se estableció en función de valor de hello del campo de tipo de Hola. Ese registro tendrá una forma diferente. A propósito, **tipo = Perf**, o **tipo = Event** también son sintaxis Hola necesita toolearn tooquery de los datos de rendimiento o eventos.

Puede usar un signo de dos puntos (:) o un signo igual (=) después de nombre de campo de Hola y antes del valor de Hola. **Type: Event** y **tipo = Event** son equivalentes en significado, puede elegir Hola estilo que prefiera.

Por lo tanto, si hello escriba = Perf registros tienen un campo llamado 'CounterName', a continuación, puede escribir una consulta parecida a `Type=Perf CounterName="% Processor Time"`.

Esto le dará solamente de los datos de rendimiento de Hola donde el nombre de contador de rendimiento de hello es "% Processor Time".

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch para datos de rendimiento de tiempo de procesador
* En el campo de consulta de búsqueda de hello, escriba`Type=Perf CounterName="% Processor Time"`

También puede ser más específico y usar **InstanceName = _ 'Total'** en consultas de hello, que es un contador de rendimiento de Windows. También puede seleccionar una faceta y otro **field:value**. filtro de Hola se agrega automáticamente tooyour filtro en la barra de consulta de Hola. Puede ver esto en hello después de la imagen. Muestra dónde tooclick tooadd **InstanceName: '_Total'** toohello consulta sin escribir nada.

![search facet](./media/log-analytics-log-searches/oms-search-facet.png)

La consulta ahora se convierte en `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

En este ejemplo, no es necesario toospecify **tipo = Perf** tooget toothis resultado. Porque Hola campos CounterName y InstanceName solo existen para los registros de tipo = Perf, consulta hello es lo suficientemente específica como tooreturn Hola mismos resultados como Hola anterior, más larga:

```
CounterName="% Processor Time" InstanceName="_Total"
```

Esto es porque todos los filtros de hello en consulta Hola se evalúan como perteneciente a *AND* entre sí. De hecho, hello más campos agregue toohello criterios, obtendrá menos resultados más específicos y refinados.

Por ejemplo, las consultas de hello `Type=Event EventLog="Windows PowerShell"` es idéntico demasiado`Type=Event AND EventLog="Windows PowerShell"`. Devuelve todos los eventos que se registraron y recopilados de registro de eventos de Windows PowerShell de Hola. Si agrega un filtro varias veces seleccionando de manera repetida Hola misma faceta, a continuación, problema de hello es meramente cosmético; podría desordenar la barra de búsqueda de hello, pero seguiría devolviendo Hola mismos resultados porque el operador AND implícito de hello siempre está ahí.

Puede invertir fácilmente el operador AND implícito de hello usando un operador NOT explícitamente. Por ejemplo:

`Type:Event NOT(EventLog:"Windows PowerShell")`o su equivalente `Type=Event EventLog!="Windows PowerShell"` devuelven todos los eventos de todos los demás registros que no son Hola registro de Windows PowerShell.

O bien, puede usar otro operador booleano como 'OR'. siguiente de Hello consulta devuelve los registros en los que Hola EventLog es Application OR System.

```
EventLog=Application OR EventLog=System
```

Con hello por encima de la consulta, obtendrá entradas para ambos registros en hello mismo conjunto de resultados.

Sin embargo, si quita hello o dejando hello AND implícito en su lugar, a continuación, hello siguiente consulta no producirá ningún resultado porque no hay una entrada de registro de eventos que pertenezca tooBOTH registros. Cada entrada de registro de eventos se escribió tooonly uno de dos registros de Hola.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Uso de filtros adicionales
Hello siguiente consulta devuelve entradas de 2 registros de eventos para todos los equipos de Hola que han enviado datos.

```
EventLog=Application OR EventLog=System
```

![search results](./media/log-analytics-log-searches/oms-search-results03.png)

Al seleccionar uno de los campos de Hola o filtros se limitará Hola consulta tooa equipo específico, sin incluir todas las demás. consulta resultante Hola se parecería al siguiente Hola.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Que es equivalente toohello siguientes, debido a hello and implícito.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Cada consulta se evalúa en hello siguiendo el orden explícito. Paréntesis de Hola de nota.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Como campo de registro de eventos de hello, puede recuperar datos únicamente de un conjunto de equipos específicos agregando o. Por ejemplo:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

De forma similar, esta Hola después de valor devuelto de la consulta **% de tiempo de CPU** Hola selecciona sólo los dos equipos.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Tipos de campo
Al crear filtros, debe comprender las diferencias de hello en trabajar con diferentes tipos de los campos devueltos por las búsquedas de registros.

Los **campos de búsqueda** se muestran en azul en los resultados de la búsqueda.  Puede usar campos de búsqueda en campo de toohello específico de condiciones de búsqueda como siguiente hello:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

Los **campos de búsqueda de texto libre** se muestran en gris en los resultados de la búsqueda.  No se utilizaron con campo de toohello específico de condiciones de búsqueda como campos de búsqueda.  Se busca solo en al realizar una consulta en todos los campos como siguiente Hola.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Operadores booleanos
Con los campos de fecha y hora, y numéricos, puede buscar valores mediante *mayor que*, *menor que* y *menor o igual que*. Puede usar operadores simples como >, <>, =, < =,! = en la barra de búsqueda de consulta de Hola.

Puede consultar un registro de eventos específico para un período de tiempo específico. Por ejemplo, hello últimas 24 horas se expresa con hello siguiente expresión mnemotécnica.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>toosearch mediante un operador booleano
* En el campo de consulta de búsqueda de hello, escriba`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)

Aunque puede controlar Hola intervalo de tiempo gráficamente, y casi siempre es recomendable toodo que, hay ventajas tooincluding un filtro de tiempo directamente en la consulta de Hola. Por ejemplo, esto funciona bien con paneles donde puede reemplazar tiempo Hola de cada icono, con independencia de hello *global* selector de tiempo en la página del panel Hola. Para obtener más información, consulte [Cuestiones sobre el tiempo en el panel](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Si desea filtrar por tiempo, tenga en cuenta que se obtienen resultados para hello *intersección* de hello dos períodos de tiempo: Hola especificada en el portal de OMS (S1) de Hola y Hola especificada en la consulta de hello (S2).

![intersección](./media/log-analytics-log-searches/oms-search-intersection.png)

Esto significa que, si hello períodos de tiempo no forman una intersección, por ejemplo en el portal de OMS Hola donde elegir **esta semana** y en la consulta de hello define **última semana**, a continuación, no hay ninguna intersección y no recibirá ningún resultado.

Operadores de comparación usados con campo de hello TimeGenerated también son útiles en otras situaciones. Por ejemplo, con los campos numéricos.

Por ejemplo, dado que las alertas de evaluación de configuración tienen Hola después de los valores de gravedad:

* 0 = Información
* 1= Advertencia
* 2 = Crítico

Puede consultar alertas de advertencia y críticas y también excluir las informativas con hello después de consulta:

```
Type=ConfigurationAlert  Severity>=1
```


También puede usar consultas por rango. Esto significa que puede proporcionar el intervalo de saludo inicial y final de los valores de una secuencia. Por ejemplo, si desea eventos del registro de eventos de Operations Manager de Hola donde hello EventID es igual o mayor que too2100 pero no superior a 2199, a continuación, Hola después consulta devolvería estos valores.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> sintaxis de intervalo de Hola que debe usar es el separador de hello dos puntos (:) field: value y *no* Hola signo de igual (=). Incluya el extremo de hello inferior y superior del intervalo de hello corchetes y sepárelos con dos puntos (..).
>
>

## <a name="manipulate-search-results"></a>Manipulación de los resultados de búsqueda
Cuando está buscando datos, podrá desea toorefine la consulta de búsqueda y tener un buen nivel de control sobre los resultados de Hola. Cuando se recuperan los resultados, puede aplicar comandos tootransform ellos.

Comandos en las búsquedas de análisis de registros *debe* seguir Hola carácter de barra vertical (|). Un filtro siempre debe ser la primera parte de una cadena de consulta de Hola. Define el conjunto de datos de hello con que trabaja y luego "canaliza" esos resultados en un comando. A continuación, puede usar comandos adicionales de hello canalización tooadd. Esto es parecido a grandes rasgos canalización de Windows PowerShell toohello.

En general, Hola lenguaje de búsqueda de análisis de registros intente toomake de estilo y los criterios de PowerShell toofollow toohello similar de TI TI los profesionales de TI y tooease Hola una curva de aprendizaje.

Los comandos tienen nombres de verbos para que pueda saber fácilmente lo que hacen.  

### <a name="sort"></a>Sort
comando de ordenación de Hello permite hello toodefine ordenación por uno o varios campos. Aunque no lo use, se aplica de forma predeterminada un tiempo en orden descendente. los resultados más recientes de Hello siempre están en parte superior de Hola de resultados de la búsqueda. Esto significa que cuando ejecuta una búsqueda con `Type=Event EventID=1234` , lo que realmente se ejecuta es:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Eso es porque es de tipo hello de experiencia con el que está familiarizado en los registros. Por ejemplo, en el Visor de eventos de Windows hello.

Puede usar a ordenación toochange Hola forma resultados se devuelven. Hello en los ejemplos siguientes muestran cómo funciona.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Hello sencillos ejemplos anteriores muestran cómo funcionan los comandos; estos cambian forma Hola de resultados de Hola Hola filtro devuelve.

### <a name="limit-and-top"></a>Limit y Top
Otro comando menos conocido es LIMIT. Limit es un verbo al estilo de PowerShell. Límite es de comando TOP toohello funcionalmente idénticas. Hello consultas siguientes devuelven Hola mismos resultados.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>toosearch con top
* En el campo de consulta de búsqueda de hello, escriba`Type=Event EventID=600 | Top 1`   
    ![search top](./media/log-analytics-log-searches/oms-search-top.png)

En la imagen de hello anterior, hay miles de 358 registros con EventID = 600. Hola campos, las facetas y filtros en hello siempre dejado de mostrar información sobre los resultados de hello devueltos *por parte de filtro de hello* de consulta de hello, que forma parte de hello delante de cualquier carácter de canalización. Hola **resultados** panel solo devuelve el resultado de hello 1 más reciente, porque comando de ejemplo de Hola en forma y transforma los resultados de Hola.

### <a name="select"></a>Seleccionar
comando SELECT Hola se comporta como Select-Object en PowerShell. Devuelve los resultados filtrados que no tienen todas sus propiedades originales. En su lugar, selecciona sólo las propiedades de Hola que especifique.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun una búsqueda con el comando select Hola
1. En el campo de búsqueda, escriba `Type=Event` y luego haga clic en **Buscar**.
2. Haga clic en **+ mostrar más** en uno de hello resultados tooview tienen todas las propiedades de Hola Hola resultados.
3. Seleccione algunas de ellas explícitamente y hello cambios de consulta demasiado`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![Búsqueda con Select](./media/log-analytics-log-searches/oms-search-select.png)

Este comando es especialmente útil cuando desea que los resultados de búsqueda de toocontrol y elegir solo un Hola partes de datos que realmente importan para la exploración, que a menudo no registro completo de Hola. También es útil cuando registros de diferentes tipos tienen *algunas* propiedades en común, pero no *todas*. Puede generar resultados con apariencia natural de una tabla o funcionan bien cuando se exportó el archivo CSV de tooa y, a continuación, se transforman en Excel.

## <a name="use-hello-measure-command"></a>Use el comando measure de Hola
MEASURE es uno de los comandos más versátiles de hello en las búsquedas de análisis de registros. Le permite tooapply estadística *funciones* tooyour datos y agregar los resultados agrupados por un campo determinado. Son muchas las funciones estadísticas que admite este comando.

### <a name="measure-count"></a>Measure count()
Hola toowork primera función estadística con y el otro toounderstand más sencilla de Hola Hola *count()* función.

Resultados de cualquier consulta de búsqueda como `Type=Event`, muestran filtros también llamados facetas en hello parte izquierda de los resultados de la búsqueda. filtros de Hello muestran una distribución de valores por un campo dado de resultados de hello en búsqueda de hello realizada.

![search measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Por ejemplo, en hello imagen anterior se verá hello **equipo** campo y se muestra que dentro de los eventos de casi 739 miles de hello en los resultados de hello, hay 68 valores únicos y distintos para hello **equipo** campo de esos registros. icono de Hello solo muestra hello 5 principales, que son Hola 5 valores más comunes que se escriben en hello **equipo** campos), ordenados por número de Hola de documentos que contienen ese valor específico en ese campo. En la imagen de hello puede ver que, entre esos casi 369 miles de eventos, 90 mil proceden hello OpsInsights04.contoso.com equipo, 83 mil del equipo de hello DB03.contoso.com y así sucesivamente.

¿Qué ocurre si desea que toosee todos los valores, ya que el icono de Hola solo muestra hello solo top 5?

Que es qué medida Hola comando puede hacer con la función count() de Hola. Esta función no usa ningún parámetro. Solo debe especificar campo hello mediante el cual desea toogroup: Hola **equipo** en este caso:

`Type=Event | Measure count() by Computer`

![search measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Sin embargo, **Computer** es simplemente un campo usado *en* cada dato; no hay ninguna base de datos relacional implicada y no hay ningún objeto **Computer** independiente en ninguna parte. Hola simplemente valores *en* Hola datos pueden describir la entidad que ha generado y otras características y aspectos de los datos de hello; por lo tanto, Hola término *faceta*. Sin embargo, también puede agrupar por otros campos. Dado que resultados originales de hello casi 739 miles de eventos de que se canalizan Hola medida comando también tienen un campo denominado **EventID**, puede aplicar Hola mismo toogroup técnica por ese campo y obtener un recuento de eventos por EventID:

```
Type=Event | Measure count() by EventID
```

Si no está interesado en número de registros real de Hola que contienen un valor específico, pero en su lugar, si desea obtener una lista de hello valores por sí mismos, puede agregar un *seleccione* comando final hello y primera columna de hello simplemente seleccione:

```
Type=Event | Measure count() by EventID | Select EventID
```

A continuación, puede obtener más intrincados y previamente ordenar resultados de hello en consultas de Hola o puede hacer clic columnas hello en cuadrícula de hello, demasiado.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch mediante measure count
* En el campo de consulta de búsqueda de hello, escriba`Type=Event | Measure count() by EventID`
* Anexar `| Select EventID` toohello final de consulta de Hola.
* Por último, anexe `| Sort EventID asc` toohello final de consulta de Hola.

Hay un par de cuestiones importantes de toonotice y resaltar:

En primer lugar, los resultados de Hola que ve ya no son Hola original sin procesar resultados. Son los resultados de agregado, básicamente grupos de resultados. Esto no supone un problema, pero debe comprender que está interactuando con una forma muy diferente de datos que difieren de forma sin formato original Hola que se crea sobre la marcha hello como resultado de la función estadística o de agregación de hello.

Segundo, **medir recuento** actualmente devuelve solo Hola top 100 primeros resultados. Este límite no aplica toohello otras funciones estadísticas. Por lo tanto, normalmente deberá toouse un toosearch de primer filtro más preciso para elementos específicos antes de aplicar measure count().

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Usar funciones max y min de Hola con comandos de medida de Hola
Son varias las situaciones en las que **Measure Max()** y **Measure Min()** son útiles. Sin embargo, puesto que cada función es opuesta entre sí, ilustraremos Max() y usted puede experimentar con Min() por su cuenta.

Si busca eventos de seguridad, tienen una propiedad **Level** que puede variar. Por ejemplo:

```
Type=SecurityEvent
```

![search measure count start](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Si desea que tooview Hola mayor valor de seguridad de hello todos eventos dados un equipo común, Hola campo Agrupar por, puede usar

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![search measure max computer](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Se mostrará que para los equipos de Hola que tenían **nivel** registros, la mayoría de ellos tiene al menos 8, el nivel muchas tenían un nivel de 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![search measure max time generated computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Esta función es muy adecuada para números, pero también para campos de fecha y hora. Resulta útil toocheck para hello última o marca de hora más reciente de cualquier parte de los datos indexados para cada equipo. ¿Por ejemplo: cuándo se notifican los eventos de seguridad más reciente de Hola para cada máquina?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Usar avg, función hello con comandos de medida de Hola
Hola función estadística Avg() usada con measure le permite el valor medio de hello toocalculate de algún campo y los resultados de grupo por hello mismo u otro campo. Esto resulta útil en muchos casos, por ejemplo, con los datos de rendimiento.

Comenzaremos con los datos de rendimiento. Tenga en cuenta que OMS actualmente recopila contadores de rendimiento tanto para equipos Windows como Linux.

toosearch para *todos los* datos de rendimiento, consulta más básica de hello es:

```
Type=Perf
```

![search avg start](./media/log-analytics-log-searches/oms-search-avg01.png)

Hola primero que notará es que el análisis de registros muestra tres perspectivas: lista, que se muestra en los que se muestran los registros reales de hello detrás de los gráficos de hello; Tabla, que muestra una vista tabular de datos del contador de rendimiento; y las métricas, que se muestran los contadores de rendimiento de gráficos para saludo.

En la imagen de hello anterior, hay dos conjuntos de campos marcados que indican Hola siguiente:

* Hola primer conjunto identifica el nombre de contador de rendimiento de Windows, el nombre del objeto y el nombre de instancia en el filtro de consulta de Hola. Estos son los campos de Hola que probablemente usará normalmente como facetas o filtros:
* **CounterValue** es Hola valor real del contador de Hola. En este ejemplo, es el valor de hello *75*.
* **TimeGenerated** es 12:51, en formato de 24 horas.

Ésta es una vista de las métricas de hello en un gráfico.

![search avg start](./media/log-analytics-log-searches/oms-search-avg02.png)

Después de leer sobre la forma de registro de rendimiento de Hola y de haber leído sobre otras técnicas de búsqueda, puede usar medida Avg() tooaggregate este tipo de datos numéricos.

A continuación se muestra un sencillo ejemplo:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![search avg samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

En este ejemplo, seleccionar contador de rendimiento de tiempo Total de CPU de Hola y el promedio por equipo. Si desea toonarrow hacia abajo el saludo de tooonly resultados últimos 6 horas, puede usar el control de filtro de tiempo de Hola o especifique en la consulta del siguiente modo:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>toosearch con avg, función hello comando measure de Hola
* En el cuadro de consulta de búsqueda de hello, escriba `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

Puede agregar y correlacionar los datos *entre* equipos. Por ejemplo, imagine que tiene un conjunto de hosts en algún tipo de granja de servidores donde cada nodo es igual tooany otro y solo lo hacen Hola todos los mismo tipo de trabajo y la carga se debe equilibrar de manera aproximada. Podría obtener sus contadores en un solo paso con hello siguiente consulta y conseguir los promedios para toda granja de Hola. Puede comenzar eligiendo los equipos de hello con hello siguiente ejemplo:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Ahora que tiene equipos de hello, también desea tooselect dos indicadores de rendimiento clave (KPI): % de uso de CPU y % espacio libre en disco. Por lo tanto, se convierte en parte de la consulta de hello:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

Ahora puede agregar equipos y contadores con el siguiente ejemplo de Hola:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Hola porque tiene una selección muy específica, **medir Avg()** comando puede devolver Hola Media no por equipo, sino en la granja de servidores de hello, simplemente Agrupar por CounterName. Por ejemplo:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Esto proporciona una vista útil compacta de un par de KPI de su entorno.

![search avg grouping](./media/log-analytics-log-searches/oms-search-avg04.png)

Puede usar fácilmente consultas de búsqueda de hello en un panel. Por ejemplo, puede guardar la consulta de búsqueda de Hola y crear un panel de llamado *KPI de granja de servidores Web*. toolearn más información acerca de los paneles, consulte [crear un panel personalizado en el análisis de registros](log-analytics-dashboards.md).

![search avg dashboard](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Utilice la función de suma de hello con el comando measure de Hola
función de suma de Hello es funciones similares de tooother del comando de medida de Hola. Puede ver un ejemplo sobre cómo toouse Hola función sum en [búsqueda de registros de IIS W3C en Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

Puede usar Max() y Min() con cadenas de texto, números, fechas y horas. Con cadenas de texto, se ordenan alfabéticamente y obtiene la primera y la última.

Sin embargo, no puede usar Sum() con campos que no sean numéricos. Esto también aplica tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Use la función de percentil de hello con el comando measure de Hola
función de percentil de Hello es tooAvg() y Sum() similares que sólo se puede utilizar para campos numéricos. Puede usar cualquier percentil entre 1 too99 en un campo numérico. También puede usar ambos comandos, **percentile** y **pct**. Estos son algunos ejemplos:  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Utilice Hola donde comando
Hola donde comando funciona como un filtro, pero se puede aplicar en el filtro de hello canalización toofurther agrega los resultados producidos por un comando de medida, como los resultados de tooraw lugar que se filtran al principio de Hola de una consulta.

Por ejemplo:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

Puede agregar otra barra vertical "|" carácter hello y dónde tooonly comando obtener equipos cuyo promedio de CPU es superior al 80%, con Hola después ejemplo:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Si está familiarizado con Microsoft System Center Operations Manager, se puede considerar Hola donde en términos de módulo de administración. Si el ejemplo de Hola fuera una regla, Hola primera parte de consulta de hello sería Hola y origen de datos de Hola donde comando sería la detección de condición de Hola.

Puede utilizar consultas de Hola como un icono en **Mi panel**, como un monitor de ordenaciones, toosee cuando CPU de los equipos están sobreutilizados. toolearn más información acerca de los paneles, consulte [crear un panel personalizado en el análisis de registros](log-analytics-dashboards.md). También puede crear y usar paneles mediante aplicación móvil de Hola. Para más información, consulte la [aplicación móvil de OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). En hello dos iconos inferiores de hello después de la imagen, puede ver Hola monitor muestra una lista y como un número. En esencia, que siempre desee Hola número toobe cero y Hola toobe lista vacía. De lo contrario, indica una condición de alerta. Si es necesario, puede usarlo tootake un vistazo qué máquinas están bajo presión.

![mobile dashboard](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Usar hello in (operador)
Hola *IN* (operador), junto con *NOT IN* permite toouse las búsquedas secundarias, que son las búsquedas que incluyen otra búsqueda como argumento. Se encierran entre llaves {} dentro de otra búsqueda *principal* o *exterior*. Hola resultado de una búsqueda secundaria, a menudo una lista de resultados diferentes, se usa como argumento en su búsqueda principal.

Puede usar las búsquedas secundarias toomatch subconjuntos de datos que no se pueden describir directamente en una expresión de búsqueda, pero que pueden generarse a partir de una búsqueda. Por ejemplo, si está interesado en usar un toofind de búsqueda de todos los eventos de *que les faltan actualizaciones de seguridad de equipos*, deberá toodesign una búsqueda secundaria que primero identifique esos *que les faltan actualizaciones de seguridad de equipos*  antes de buscar los eventos que pertenecen toothose hosts.

Por lo tanto, puede expresar *necesitan de equipos que les faltan actualmente actualizaciones de seguridad* con hello después de consulta:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Una vez que tenga la lista de hello, puede usar búsqueda de hello como una lista de búsqueda interna toofeed Hola de equipos en una búsqueda externa (principal) que buscará eventos de esos equipos. Para ello escriba búsqueda interna Hola entre llaves e incorpore sus resultados como valores posibles de un campo o filtro en búsqueda externa hello mediante operador IN de Hola. consulta de Hello sería algo parecido a:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

También tiempo de Hola de aviso de filtro que se utiliza en la búsqueda interna Hola porque Hola evaluación de actualización del sistema toma una instantánea de todos los equipos cada 24 horas. Puede realizar la consulta interna de hello más ligera y precisa si solo busca un día. búsqueda externa Hello en su lugar usa selección de tiempo de hello en la interfaz de usuario de hello, recupera eventos de hello últimos 7 días. Consulte [Operadores booleanos](#boolean-operators) para más información acerca de los operadores de tiempo.

Dado que realmente solo Hola usar los resultados de búsqueda interna de Hola como un valor de filtro para Hola externa, puede aplicar comandos en búsqueda externa Hola. Por ejemplo, todavía puede Hola de grupo por encima de los eventos con otro comando measure:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

Por lo general, desea que la consulta interna tooexecute rápidamente porque el análisis de registro tiene tiempos de espera del servicio para y también tooreturn una pequeña cantidad de resultados. Si la consulta interna de hello devuelve más resultados, se trunca lista de resultados de Hola Hola búsqueda externa tooreturn potencialmente que podría producir resultados incorrectos.

Otra regla es que la búsqueda interna de hello necesita actualmente tooprovide *agregados* resultados. Es decir, debe contener un comando *measure* ; actualmente no se pueden proporcionar resultados sin procesar a una búsqueda externa.

Además, puede haber solo un operador IN y este debe ser Hola último filtro de consulta de Hola. No pueden tener varios operadores IN o haría: Esto se evita básicamente ejecuta varias búsquedas secundarias;: Hola importante punto es que solo una búsqueda secundaria o interna es posible para cada búsqueda externa.

Incluso con estos límites, IN permite realizar muchos tipos de búsquedas correlacionadas y le permite toodefine toogroups algo similar como equipos, usuarios o archivos: los campos de hello en los datos contienen. Estos son otros ejemplos:

**Todas las actualizaciones que faltan en equipos donde se deshabilitó la configuración Actualización automática**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Todos los eventos de error de equipos que ejecutan SQL Server (=donde se ejecutó la evaluación de SQL)**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Todos los eventos de seguridad de equipos que son controladores de dominio (=donde se ejecutó la evaluación de AD)**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**¿Qué otras cuentas han iniciado sesión en toohello mismos equipos que cuenta BACONLAND\jochan ha iniciado sesión?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Use el comando distinct de Hola
Como sugiere su nombre hello, este comando proporciona una lista de valores distintos para un campo. Es sorprendentemente sencillo pero muy útil. Hola que se puede lograr mismo con el comando measure count() así, como se muestra a continuación.

```
Type=Event | Measure count() by Computer
```

![Ejemplo del comando de búsqueda DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Sin embargo, si todo lo que le interesa es una lista de valores distintos y no Hola número de documentos que tengan que los valores, a continuación, DISTINCT puede proporcionar tooread más limpio y más fácil de salida y una sintaxis más corta, tal y como se muestra a continuación.

```
Type=Event | Distinct Computer
```
![Ejemplo del comando de búsqueda DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Usar función countdistinct de hello con comandos de medida de Hola
función countdistinct de Hello cuenta número Hola de valores distintos dentro de cada grupo. Por ejemplo, es posible usar toocount Hola un número de equipos únicos reporting para cada tipo:

```
* | measure countdistinct(Computer) by Type
```

![Countdistinct de OMS](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Usar comandos de intervalo de medida de Hola
Con una recopilación de datos de rendimiento prácticamente en tiempo real, puede recopilar y visualizar cualquier contador de rendimiento en Log Analytics. Basta con escribir consultas de hello **tipo: rendimiento** devolverá miles de métricas gráficos según el número de Hola de contadores y los servidores en su entorno de análisis de registros. Con la agregación de métricas a petición, puede mirar Hola métricas generales en su entorno en un nivel alto y profundización en los datos más pormenorizados que necesite.

Supongamos que desea tooknow ¿qué es el promedio de CPU de hello en todos los equipos. Examinando Hola CPU promedio para cada equipo podría no ser útil porque pueden obtener atenuados resultados. toolook con mayor detalle, puede agrupar el resultado en un momento más pequeño fragmentos de ventana y buscar en una serie de tiempo en distintas dimensiones. Por ejemplo, puede realizar por hora media de hello del uso de CPU a través de todos los equipos como se indica a continuación:

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Medida de promedios en un intervalo](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

De forma predeterminada, estos resultados se mostrarán en un gráfico de líneas interactivo con varias series.  Este gráfico admite alternar entre series (con el cambio de escala del eje Y), usar el zoom y mantener el mouse sobre elementos.  opción de visualización de tabla Hola está todavía disponible para ver los datos sin procesar de hello si es necesario.

También puede agrupar por otros campos. En este ejemplo, que me interesa en todos los contadores % de Hola para un equipo específico y deseo tooknow: ¿qué es cada hora 70 percentiles de Hola de cada contador:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Una toonote lo es que estas consultas no son contadores tooperformance limitado. Se puede aplicar tooany métrica. En este ejemplo, estoy consultando los registros de IIS para W3C. Deseo tooknow ¿qué es el tiempo máximo de hello necesario en un intervalo de 5 minutos para procesar cada solicitud:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Uso de varios agregados en una consulta
Puede especificar varias cláusulas de agregado en un comando measure.  A cada una se le puede asignar un alias de forma independiente.  Si no se proporciona un alias resultante de hello nombre del campo será la función de agregado de Hola que usó (es decir, "avg(CounterValue)" para avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![Varios agregados en OMS 1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Este es otro ejemplo:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Pasos siguientes
Para más información acerca de las búsquedas de registros, consulte:

* Use [campos personalizados en el análisis de registros](log-analytics-custom-fields.md) tooextend búsquedas de registros.
* Hola de revisión [referencia de búsqueda de registro de análisis de registros](log-analytics-search-reference.md) tooview todos Hola buscar campos y facetas disponibles en el análisis de registros.
