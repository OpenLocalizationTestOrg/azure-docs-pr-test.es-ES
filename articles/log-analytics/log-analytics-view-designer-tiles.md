---
title: "referencia de aaaTile para el Diseñador de vistas de análisis de registros de OMS | Documentos de Microsoft"
description: "Diseñador de vistas de análisis de registros permite toocreate personalizar vistas de consola OMS de Hola que contienen diferentes visualizaciones de datos en el repositorio OMS Hola. En este artículo se proporciona una referencia de configuración de Hola para cada uno de los iconos disponibles toouse de hello en sus vistas personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Referencia de los iconos del Diseñador de vistas de Log Analytics
Hola Diseñador de vistas de análisis de registros permite toocreate personalizado vistas de consola OMS de Hola que contienen diferentes visualizaciones de datos en el repositorio OMS Hola. En este artículo se proporciona una referencia de configuración de Hola para cada uno de los iconos disponibles toouse de hello en sus vistas personalizadas.

Estos son otros de los artículos disponibles sobre el Diseñador de vistas:

* [Ver diseñador](log-analytics-view-designer.md) -información general de hello Diseñador de vistas y procedimientos para crear y editar vistas personalizadas.
* [Referencia de elemento de visualización](log-analytics-view-designer-parts.md) -referencia de configuración de Hola para cada uno de hello iconos toouse disponible en sus vistas personalizadas.

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, se deben escribir consultas en todas las vistas en hello [nuevo lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas las vistas que se crearon antes de que se actualizó el área de trabajo de hello será automáticamente convertido.

Hello tabla siguiente enumeran tipos diferentes de hello de iconos disponibles en el Diseñador de vistas de Hola.  Hola las siguientes secciones describen cada tipo de mosaico en detalle y sus propiedades.

| Icono | Descripción |
|:--- |:--- |
| [Number](#number-tile) |Un solo número que muestra la cantidad de registros de una consulta. |
| [Dos números](#two-numbers-tile) |Dos números que muestra las cantidades de registros de dos consultas diferentes. |
| [Anillo](#donut-tile) |Gráfico de anillos basado en una consulta con un valor de resumen en el centro de Hola. |
| [Llamada de gráfico de líneas](#line-chart-amp-callout-tile) |Gráfico de líneas basado en una consulta y una llamada con un valor de resumen. |
| [Gráfico de líneas](#line-chart-tile) |Gráfico de líneas basado en una consulta. |
| [Dos escalas de tiempo](#two-timelines-tile) |Gráfico de columnas con dos series, cada una de ellas basada en una consulta independiente. |

## <a name="number-tile"></a>Icono de Número
Hola **número** mosaico muestra un único número que muestra el recuento de Hola de registros de una consulta de registro y una etiqueta.

![Icono de Número](media/log-analytics-view-designer/tile-number.png)

| Configuración | Descripción |
|:--- |:--- |
| Nombre |Icono texto toodisplay princip Hola Hola. |
| Descripción |Texto toodisplay en nombre del mosaico Hola. |
| **Icono** | |
| Leyenda |Toodisplay de texto en el valor de Hola. |
| Consultar |Toorun de consulta.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| **Avanzado** |**&gt; Comprobación del flujo de datos** |
| habilitado |Seleccione si la comprobación de flujo de datos debe habilitarse para el icono de Hola.  Esto proporciona un mensaje alternativo si no hay datos de mosaico de Hola.  Se trata de tooprovide usado normalmente un mensaje durante el período temporal de hello cuando se instala la vista de Hola y datos proceden disponibles. |
| Consultar |Consultar toorun toocheck si los datos están disponibles para la vista de Hola.  Si consulta hello no devuelve ningún resultado, se muestra un mensaje en lugar de valor de Hola de consulta principal Hola. |
| Message |Mensaje toodisplay si consulta de comprobación de flujo de datos de hello no devuelve ningún dato.  Si no proporciona ningún mensaje, se mostrará *Realizando evaluación*. |


## <a name="two-numbers-tile"></a>Icono de Dos números
Hola **número dos** icono muestra que muestra el recuento de Hola de registros de una etiqueta y dos consultas de registro diferente para cada uno de dos números.

![Icono de Dos números](media/log-analytics-view-designer/tile-two-numbers.png)

| Configuración | Descripción |
|:--- |:--- |
| Nombre |Icono texto toodisplay princip Hola Hola. |
| Descripción |Texto toodisplay en nombre del mosaico Hola. |
| **Primer icono** | |
| Leyenda |Toodisplay de texto en el valor de Hola. |
| Consultar |Toorun de consulta.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| **Segundo icono** | |
| Leyenda |Toodisplay de texto en el valor de Hola. |
| Consultar |Toorun de consulta.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| **Avanzado** |**&gt; Comprobación del flujo de datos** |
| habilitado |Seleccione si la comprobación de flujo de datos debe habilitarse para el icono de Hola.  Esto proporciona un mensaje alternativo si no hay datos de mosaico de Hola.  Se trata de tooprovide usado normalmente un mensaje durante el período temporal de hello cuando se instala la vista de Hola y datos proceden disponibles. |
| Consultar |Consultar toorun toocheck si los datos están disponibles para la vista de Hola.  Si consulta hello no devuelve ningún resultado, se muestra un mensaje en lugar de valor de Hola de consulta principal Hola. |
| Message |Mensaje toodisplay si consulta de comprobación de flujo de datos de hello no devuelve ningún dato.  Si no proporciona ningún mensaje, se mostrará *Realizando evaluación*. |


## <a name="donut-tile"></a>Icono Anillo
Hola **anillo** mosaico muestra un número único que se resumen a partir de una columna de valor en una consulta de registro.  anillo de Hello gráficamente muestra resultados de registros de tres principales Hola.

![Icono Anillo](media/log-analytics-view-designer/tile-donut.png)

| Configuración | Descripción |
|:--- |:--- |
| Nombre |Icono texto toodisplay princip Hola Hola. |
| Descripción |Texto toodisplay en nombre del mosaico Hola. |
| **Anillo** | |
| Consultar |Consultar toorun para anillos de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Esto suele ser una consulta que utiliza hello **medida** resultados de toosummarize de palabra clave. |
| **Anillo** |**&gt; Centro** |
| Texto |Toodisplay de texto en el valor dentro de anillo de Hola Hola. |
| Operación |Hola tooperform operación en un único valor de hello valor propiedad toosummarize tooa.<br><br>-Sum: Agregar valores de hello de todos los registros con el valor de la propiedad de Hola.<br>-Porcentaje: Porcentaje de valores de hello sumada de registros con hello propiedad valor compara toohello suma los valores de todos los registros. |
| Valores de resultado usados en la operación central |Opcionalmente, haga clic en Hola signo tooadd uno o varios valores.  resultados de Hola de consulta de hello serán toorecords limitado con valores de propiedad de Hola que especifique.  Si no se agrega ningún valor, que todos los registros se incluyen en la consulta de Hola. |
| **Anillo** |**&gt; Opciones adicionales** |
| Colores |Hola toodisplay de color para cada uno de tres propiedades principales de Hola.  Si desea colores alternativos toospecify para los valores de propiedad específica, utilice, a continuación, asignación avanzada de Color. |
| Asignación de color avanzada |Muestra un color para valores de propiedad concretos.  Si el valor de hello especificado está en Hola tres principales, a continuación, un color diferente Hola se muestra en lugar de color estándar de Hola.  Si la propiedad de hello no está en Hola tres principales, a continuación, no se muestra el color de Hola. |
| **Avanzado** |**&gt; Comprobación del flujo de datos** |
| habilitado |Seleccione si la comprobación de flujo de datos debe habilitarse para el icono de Hola.  Esto proporciona un mensaje alternativo si no hay datos de mosaico de Hola.  Se trata de tooprovide usado normalmente un mensaje durante el período temporal de hello cuando se instala la vista de Hola y datos proceden disponibles. |
| Consultar |Consultar toorun toocheck si los datos están disponibles para la vista de Hola.  Si consulta hello no devuelve ningún resultado, se muestra un mensaje en lugar de valor de Hola de consulta principal Hola. |
| Message |Mensaje toodisplay si consulta de comprobación de flujo de datos de hello no devuelve ningún dato.  Si no proporciona ningún mensaje, se mostrará *Realizando evaluación*. |


## <a name="line-chart-tile"></a>Icono de Gráfico de líneas
Hola **gráfico de líneas** mosaico muestra un gráfico de líneas con varias series de una consulta de registro con el tiempo.  

![Icono de Llamada de gráfico de líneas](media/log-analytics-view-designer/tile-line-chart.png)

| Configuración | Descripción |
|:--- |:--- |
| Nombre |Icono texto toodisplay princip Hola Hola. |
| Descripción |Texto toodisplay en nombre del mosaico Hola. |
| **Gráfico de líneas** | |
| Consultar |Toorun de consulta para el gráfico de líneas de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Esto suele ser una consulta que utiliza hello **medida** resultados de toosummarize de palabra clave.  Si la consulta de hello utiliza hello **intervalo** (palabra clave), a continuación, Hola eje x del gráfico de hello usará este intervalo de tiempo.  Si consulta hello no incluye hello **intervalo** intervalos de palabra clave, a continuación, cada hora se usan para saludo del eje x. |
| **Gráfico de líneas** |**&gt; Eje Y** |
| Usar escala logarítmica |Seleccione toouse una escala logarítmica para hello eje y. |
| Unidades |Especifique unidades de Hola para los valores de hello devueltos por la consulta de Hola.  Esta información es toodisplay usa etiquetas en el gráfico de Hola que indica los tipos de valor de hello y, opcionalmente, para convertir los valores de hello.  Hola **tipo de unidad** especifica la categoría de Hola de unidad de Hola y define hello **tipo de unidad actual** valores que están disponibles.  Si selecciona un valor en **convertir en** , a continuación, se convierten los valores numéricos de Hola de hello **unidad actual** escriba toohello **convertir en** tipo. |
| Etiqueta personalizada |Texto toodisplay para hello Y siguiente toohello etiqueta de eje para el tipo de unidad de Hola.  Si no se especifica ninguna etiqueta, se muestra sólo el tipo de unidad Hola. |
| **Avanzado** |**&gt; Comprobación del flujo de datos** |
| habilitado |Seleccione si la comprobación de flujo de datos debe habilitarse para el icono de Hola.  Esto proporciona un mensaje alternativo si no hay datos de mosaico de Hola.  Se trata de tooprovide usado normalmente un mensaje durante el período temporal de hello cuando se instala la vista de Hola y datos proceden disponibles. |
| Consultar |Consultar toorun toocheck si los datos están disponibles para la vista de Hola.  Si consulta hello no devuelve ningún resultado, se muestra un mensaje en lugar de valor de Hola de consulta principal Hola. |
| Message |Mensaje toodisplay si consulta de comprobación de flujo de datos de hello no devuelve ningún dato.  Si no proporciona ningún mensaje, se mostrará *Realizando evaluación*. |


## <a name="line-chart--callout-tile"></a>Icono de Llamada de gráfico de líneas
Hola **gráfico & llamada línea** mosaico muestra un gráfico de líneas con varias series de una consulta de registro con el tiempo y una llamada con un valor resumido.  

![Icono de Llamada de gráfico de líneas](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Configuración | Descripción |
|:--- |:--- |
| Nombre |Icono texto toodisplay princip Hola Hola. |
| Descripción |Texto toodisplay en nombre del mosaico Hola. |
| **Gráfico de líneas** | |
| Consultar |Toorun de consulta para el gráfico de líneas de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Esto suele ser una consulta que utiliza hello **medida** resultados de toosummarize de palabra clave.  Si la consulta de hello utiliza hello **intervalo** (palabra clave), a continuación, Hola eje x del gráfico de hello usará este intervalo de tiempo.  Si consulta hello no incluye hello **intervalo** intervalos de palabra clave, a continuación, cada hora se usan para saludo del eje x. |
| **Gráfico de líneas** |**&gt; Llamada** |
| Llamada |Toodisplay de texto de título por encima del valor de la llamada de Hola. |
| Nombre de la serie |Valor de propiedad para toouse de serie de hello para el valor de la llamada de Hola.  Si no se proporciona ninguna serie, se utilizan todos los registros de consulta de Hola. |
| Operación |Hola tooperform operación en hello valor toosummarize tooa único valor de propiedad para la llamada de Hola.<br>-Promedio: El promedio del valor de Hola de todos los registros.<br><br>-Recuento: El recuento de todos los registros devueltos por la consulta de Hola.<br>-Último ejemplo: El valor del último intervalo de hello incluido en el gráfico de Hola.<br>-Max: Valor de máximo uno de los intervalos de hello incluidos en el gráfico de Hola.<br>-Mínimo: Valor mínimo uno de los intervalos de hello incluidos en el gráfico de Hola.<br>-Sum: Suma del valor de Hola de todos los registros. |
| **Gráfico de líneas** |**&gt; Eje Y** |
| Usar escala logarítmica |Seleccione toouse una escala logarítmica para hello eje y. |
| Unidades |Especifique unidades de Hola para los valores de hello devueltos por la consulta de Hola.  Esta información es toodisplay usa etiquetas en el gráfico de Hola que indica los tipos de valor de hello y, opcionalmente, para convertir los valores de hello.  Hola **tipo de unidad** especifica la categoría de Hola de unidad de Hola y define hello **tipo de unidad actual** valores que están disponibles.  Si selecciona un valor en **convertir en** , a continuación, se convierten los valores numéricos de Hola de hello **unidad actual** escriba toohello **convertir en** tipo. |
| Etiqueta personalizada |Texto toodisplay para hello Y siguiente toohello etiqueta de eje para el tipo de unidad de Hola.  Si no se especifica ninguna etiqueta, se muestra sólo el tipo de unidad Hola. |
| **Avanzado** |**&gt; Comprobación del flujo de datos** |
| habilitado |Seleccione si la comprobación de flujo de datos debe habilitarse para el icono de Hola.  Esto proporciona un mensaje alternativo si no hay datos de mosaico de Hola.  Se trata de tooprovide usado normalmente un mensaje durante el período temporal de hello cuando se instala la vista de Hola y datos proceden disponibles. |
| Consultar |Consultar toorun toocheck si los datos están disponibles para la vista de Hola.  Si consulta hello no devuelve ningún resultado, se muestra un mensaje en lugar de valor de Hola de consulta principal Hola. |
| Message |Mensaje toodisplay si consulta de comprobación de flujo de datos de hello no devuelve ningún dato.  Si no proporciona ningún mensaje, se mostrará *Realizando evaluación*. |


## <a name="two-timelines-tile"></a>Icono de Dos escalas de tiempo
Hola **dos escalas de tiempo** mosaico muestra los resultados de Hola de dos consultas de registro con el tiempo como gráficos de columnas.  Para cada serie, se muestra una llamada.  

![Icono de Dos escalas de tiempo](media/log-analytics-view-designer/tile-two-timelines.png)

| Configuración | Descripción |
|:--- |:--- |
| Nombre |Icono texto toodisplay princip Hola Hola. |
| Descripción |Texto toodisplay en nombre del mosaico Hola. |
| Primer gráfico | |
| Leyenda |Toodisplay de texto en la llamada de hello para la primera serie de Hola. |
| Color |Toouse de color para las columnas de hello en la primera serie de Hola. |
| Consulta de gráfico |Toorun de consulta para la primera serie de Hola.  recuento de Hello del número de Hola de registros en cada intervalo de tiempo se representará mediante columnas de gráfico de Hola. |
| Operación |Hola tooperform operación en hello valor toosummarize tooa único valor de propiedad para la llamada de Hola.<br><br>-Promedio: El promedio del valor de Hola de todos los registros.<br>-Recuento: El recuento de todos los registros devueltos por la consulta de Hola.<br>-Último ejemplo: El valor del último intervalo de hello incluido en el gráfico de Hola.<br>-Max: Valor de máximo uno de los intervalos de hello incluidos en el gráfico de Hola. |
| **Segundo gráfico** | |
| Leyenda |Toodisplay de texto en la llamada de hello para la segunda serie de Hola. |
| Color |Toouse de color para las columnas de hello en la segunda serie de Hola. |
| Consulta de gráfico |Toorun de consulta para la segunda serie de Hola.  recuento de Hello del número de Hola de registros en cada intervalo de tiempo se representará mediante columnas de gráfico de Hola. |
| Operación |Hola tooperform operación en hello valor toosummarize tooa único valor de propiedad para la llamada de Hola.<br><br>-Promedio: El promedio del valor de Hola de todos los registros.<br>-Recuento: El recuento de todos los registros devueltos por la consulta de Hola.<br>-Último ejemplo: El valor del último intervalo de hello incluido en el gráfico de Hola.<br>-Max: Valor de máximo uno de los intervalos de hello incluidos en el gráfico de Hola. |
| **Avanzado** |**&gt; Comprobación del flujo de datos** |
| habilitado |Seleccione si la comprobación de flujo de datos debe habilitarse para el icono de Hola.  Esto proporciona un mensaje alternativo si no hay datos de mosaico de Hola.  Se trata de tooprovide usado normalmente un mensaje durante el período temporal de hello cuando se instala la vista de Hola y datos proceden disponibles. |
| Consultar |Consultar toorun toocheck si los datos están disponibles para la vista de Hola.  Si consulta hello no devuelve ningún resultado, se muestra un mensaje en lugar de valor de Hola de consulta principal Hola. |
| Message |Mensaje toodisplay si consulta de comprobación de flujo de datos de hello no devuelve ningún dato.  Si no proporciona ningún mensaje, se mostrará *Realizando evaluación*. |


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) toosupport consultas de hello en mosaicos.
* Agregar [elementos de visualización](log-analytics-view-designer-parts.md) tooyour de vista personalizada.
