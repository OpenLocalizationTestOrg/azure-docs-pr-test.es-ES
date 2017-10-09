---
title: "portal de la búsqueda de registro aaaUsing hello en análisis de registros de Azure | Documentos de Microsoft"
description: "Este artículo incluye un tutorial que describe cómo toocreate búsquedas de registro y analizar los datos almacenados en el área de trabajo de análisis de registros mediante el portal de la búsqueda de registro de hello.  tutorial de Hello incluye ejecutan algunas consultas sencillas tooreturn diferentes tipos de datos y analizar los resultados."
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
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Crear búsquedas de registros de análisis de registros de Azure mediante el portal de la búsqueda de registro de hello

> [!NOTE]
> Este artículo describe portal de búsqueda de registros de hello en análisis de registros de Azure mediante el lenguaje de consulta nueva Hola.  Puede obtener más información sobre el nuevo lenguaje de Hola y obtener Hola procedimiento tooupgrade el área de trabajo en [actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).  
>
> Si el área de trabajo no se ha actualizado toohello nuevo lenguaje de consulta, se debe hacer referencia demasiado[buscar datos mediante búsquedas de registros de análisis de registros](log-analytics-log-searches.md) para obtener información sobre la versión actual de Hola de portal de la búsqueda de registro de hello.

Este artículo incluye un tutorial que describe cómo toocreate búsquedas de registro y analizar los datos almacenados en el área de trabajo de análisis de registros mediante el portal de la búsqueda de registro de hello.  tutorial de Hello incluye ejecutan algunas consultas sencillas tooreturn diferentes tipos de datos y analizar los resultados.  Se centra en características de portal de la búsqueda de registros de Hola para modificar la consulta de hello en lugar de modificarlo directamente.  Para obtener más información acerca de cómo modificar directamente consultas hello, vea hello [referencia del lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856079).

toocreate realiza una búsqueda en portal de análisis avanzado de hello en lugar de portal de la búsqueda de registro de hello, consulte [Getting Started with Hola Portal de análisis](https://go.microsoft.com/fwlink/?linkid=856587).  Ambos portales usar hello misma consulta lenguaje tooaccess Hola mismos datos en el área de trabajo de análisis de registros de Hola.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial se da por supuesto que ya tiene un área de trabajo de análisis de registros con al menos un origen conectado que genera los datos de hello consultas tooanalyze.  

- Si no tiene un área de trabajo, puede crear uno mediante el procedimiento de hello en [empezar a trabajar con un área de trabajo de análisis de registros](log-analytics-get-started.md).
- Conecte uno menos [el agente de Windows](log-analytics-windows-agents.md) o un [agente Linux](log-analytics-linux-agents.md) toohello área de trabajo.  

## <a name="open-hello-log-search-portal"></a>Portal de la búsqueda de registro de hello abierto
Empiece por abrir el portal de la búsqueda de registros de Hola.  Puede acceder a ella de hello portal de Azure o portal de OMS Hola.

1. Hola abrir portal de Azure.
2. Desplácese tooLog análisis y seleccione el área de trabajo.
3. Seleccionar una opción **Log Search** toostay Hola portal o inicie Hola OMS portal de Azure seleccionando **Portal de OMS** y, a continuación, haga clic en botón de búsqueda de registros de Hola.

![Botón Log Search (Búsqueda de registros)](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Creación de una búsqueda simple
tooretrieve de manera más rápida de Hello algunos toowork de datos con es una consulta simple que devuelve todos los registros en la tabla.  Si dispone de todas las ventanas o los clientes de Linux conectados tooyour área de trabajo, tendrá que datos de Hola o eventos (Windows) o una tabla de Syslog (Linux).

Escriba un hello las siguientes consultas en el cuadro de búsqueda de Hola y haga clic en el botón de búsqueda de Hola.  

```
Event
```
```
Syslog
```

Se devuelven los datos en la vista de lista predeterminada de Hola y puede ver el número total de registros se han devuelto.

![Consulta sencilla](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Solo hello primera algunas propiedades de cada registro se muestran.  Haga clic en **mostrar más** toodisplay todas las propiedades de un registro concreto.

![Detalles del registro](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Establecer el ámbito de la hora de Hola
Cada registro recopilado por el análisis de registro tiene una **TimeGenerated** propiedad que contiene Hola fecha y hora en que se creó ese registro Hola.  Una consulta en el portal de la búsqueda de registro de hello solo devuelve los registros con un **TimeGenerated** ámbito Hola tiempo que se muestra en la parte izquierda de la pantalla de bienvenida de Hola.  

Puede cambiar filtro de tiempo de hello mediante la selección de la lista desplegable de Hola o modificando el control deslizante de Hola.  control deslizante de Hello muestra un gráfico de barras que muestra hello relativa número de registros para cada segmento de tiempo de intervalo de saludo.  Este segmento variará según el intervalo de saludo.

ámbito de tiempo predeterminado de Hello es **1 día**.  Cambie este valor demasiado**7 días**, y debe aumentar el número total de Hola de registros.

![Ámbito de tiempo y fecha](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Filtrar los resultados de consulta de Hola
En hello lado izquierdo de la pantalla de bienvenida es el panel de filtro de Hola que permite tooadd filtrado de la consulta toohello sin modificarlo directamente.  Varias propiedades de registros de hello devueltos se muestran con sus valores superiores diez con su número de registros.

Si está trabajando con **eventos**, seleccione Hola casilla de verificación junto a demasiado**Error** en **EVENTLEVELNAME**.   Si está trabajando con **Syslog**, seleccione Hola casilla de verificación junto a demasiado**err** en **SEVERITYLEVEL**.  Esto cambia la consulta de hello tooone de hello después toolimit Hola provoca eventos tooerror.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtrar](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Panel de filtro de agregar propiedades toohello seleccionando **agregar toofilters** desde el menú de la propiedad de hello en uno de los registros de Hola.

![Agregar menús toofilter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

Puede establecer Hola mismo filtro seleccionando **filtro** desde el menú de la propiedad de Hola para un registro con el valor de hello desea toofilter.  

Solo tiene hello **filtro** opción de propiedades con su nombre en azul.  Se trata de campos que permiten *búsquedas* que se indexan para las condiciones de búsqueda.  Campos en gris son *permite realizar búsquedas de texto libre* los campos que solo tienen hello **mostrar referencias** opción.  Esta opción devuelve los registros que contienen ese valor en cualquier propiedad.

![Menú Filtrar](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Puede agrupar los resultados de hello en una sola propiedad seleccionando hello **Agrupar por** opción en el menú del registro de hello.  Esto agregará una [resumir](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) consulta tooyour de operador que muestra los resultados de hello en un gráfico.  Puede agrupar por más de una propiedad, pero debe generar consulta de hello tooedit directamente.  Siguiente Hola Hola del menú Registro Hola seleccione **equipo** propiedad y seleccione **Group by 'Computer'**.  

![Agrupar por equipo](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Trabajo con resultados
portal de la búsqueda de registro de Hello tiene una variedad de características para trabajar con hello los resultados de una consulta.  Puede ordenar, filtrar y agrupar datos de resultados de tooanalyze Hola sin modificar la consulta real Hola.  Los resultados de una consulta no se ordenan de forma predeterminada.

tooview Hola datos en forma de tabla que proporciona opciones adicionales para filtrar y ordenar, haga clic en **tabla**.  

![Vista Tabla](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Haga clic en la flecha de Hola por un detalles de hello tooview registros para ese registro.

![Ordenar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Ordene cualquier campo haciendo clic en el encabezado de la columna.

![Ordenar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Filtrar los resultados de hello en un valor específico en la columna de hello haciendo clic en el botón de filtro de Hola y proporcionar una condición de filtro.

![Filtrar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Agrupar en una columna arrastrando su parte superior toohello de encabezado de columna de resultados de Hola.  Puede agrupar por varios campos, arrastre la parte superior toohello de varias columnas.

![Agrupar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Trabajo con datos de rendimiento
Los datos de rendimiento para los agentes de Windows y Linux se almacenan en el área de trabajo de análisis de registros de Hola Hola **rendimiento** tabla.  Los registros de rendimiento tienen la misma apariencia que cualquier otro registro y puede escribir una consulta sencilla que devuelva todos los datos de rendimiento igual que se hace con los eventos.

```
Perf
```

![Datos de rendimiento](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

La devolución de millones de registros para todos los objetos y contadores de rendimiento no resulta muy útil.  Puede usar Hola mismos métodos usados por encima de los datos de hello toofilter o simplemente escriba Hola siguiente consultar directamente en el cuadro de búsqueda de registro de hello.  Esta devolverá únicamente los registros de utilización del procesador para los equipos con Windows y Linux.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilización del procesador](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Esto limita el contador de hello datos tooa determinado, pero aún no lo coloque en un formulario que es especialmente útil.  Puede mostrar los datos de hello en un gráfico de líneas, pero primero debe toogroup por equipo y TimeGenerated.  toogroup por varios campos, es necesario tener toomodify Hola query directamente, por lo que modificar Hola consulta toohello.  Esto utiliza hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) función hello **CounterValue** propiedad toocalculate Hola promedio durante cada hora.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Gráfico con datos de rendimiento](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Ahora que los datos de hello convenientemente están agrupados, puede mostrar en un gráfico visual agregando hello [representar](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operador.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Gráfico de líneas](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Pasos siguientes

- Obtener más información sobre el lenguaje de consulta de análisis de registros de hello en [Getting Started with Hola Portal de análisis](https://go.microsoft.com/fwlink/?linkid=856079).
- Ver un tutorial con hello [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) que le permite toorun Hola mismo las consultas y acceso Hola mismos datos que el portal de la búsqueda de registros de Hola.
