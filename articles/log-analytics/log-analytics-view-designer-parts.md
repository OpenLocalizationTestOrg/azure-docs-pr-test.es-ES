---
title: "referencia de aaaPart para el Diseñador de vistas de análisis de registros de OMS | Documentos de Microsoft"
description: "Diseñador de vistas de análisis de registros permite toocreate personalizar vistas de consola OMS de Hola que contienen diferentes visualizaciones de datos en el repositorio OMS Hola. En este artículo se proporciona una referencia de configuración de Hola para cada uno de los elementos de visualización Hola disponible toouse en sus vistas personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Referencia de los elementos de visualización del Diseñador de vistas de Log Analytics
Hola Diseñador de vistas de análisis de registros permite toocreate vistas personalizadas en la consola de OMS de Hola que contienen diferentes visualizaciones de datos de repositorio de OMS Hola. En este artículo se proporciona una referencia de configuración de Hola para cada uno de los elementos de visualización Hola disponible toouse en sus vistas personalizadas.

Estos son otros de los artículos disponibles sobre el Diseñador de vistas:

* [Ver diseñador](log-analytics-view-designer.md) -información general de hello Diseñador de vistas y procedimientos para crear y editar vistas personalizadas.
* [Icono referencia](log-analytics-view-designer-tiles.md) -referencia de configuración de Hola para cada uno de hello iconos toouse disponible en sus vistas personalizadas.

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, se deben escribir consultas en todas las vistas en hello [nuevo lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas las vistas que se crearon antes de que se actualizó el área de trabajo de hello será automáticamente convertido.

Hello tabla siguiente describen distintos tipos de iconos disponibles en el Diseñador de vistas de Hola de Hola.  Hola las siguientes secciones describen cada tipo de mosaico en detalle y sus propiedades.

| Tipo de vista | Descripción |
|:--- |:--- |
| [Lista de consultas](#list-of-queries-part) |Muestra una lista de las consultas de búsqueda de registros.  Hola usuario puede hacer clic en cada consulta toodisplay sus resultados. |
| [Number &amp; list](#number-amp-list-part) (Número y lista) |El encabezado tiene un solo número que muestra la cantidad de registros de una consulta de búsqueda de registros.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo. |
| [Dos números y lista](#two-numbers-amp-list-part) |El encabezado tiene dos números que muestran la cantidad de registros de consultas de búsqueda de registros independientes.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo. |
| [Donut &amp; list](#donut-amp-list-part) (Anillo y lista) |El encabezado muestra un solo número resumido obtenido a partir de una columna de valor de una consulta de registros.  anillo de Hello gráficamente muestra resultados de registros de tres principales Hola. |
| [Dos escalas de tiempo y lista](#two-timelines-amp-list-part) |Encabezado muestra hello resultados de las consultas de dos registros con el tiempo como gráficos de columnas con una llamada de mostrar un número único de resumen a partir de una columna de valor en una consulta de registro.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo. |
| [Información](#information-part) |El encabezado muestra texto estático y un vínculo opcional.  La lista muestra uno o varios elementos con texto estático y un título. |
| [Gráfico de líneas, llamada, lista](#line-chart-callout-amp-list-part) |El encabezado muestra un gráfico de líneas con varias series de una consulta de registro en un periodo y una llamada con un valor resumido.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo. |
| [Gráfico de líneas y lista](#line-chart-amp-list-part) |El encabezado muestra un gráfico de líneas con varias series de una consulta de registro en un periodo.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo. |
| [Elemento Stack of line charts (Pila de gráficos de líneas)](#stack-of-line-charts-part) |Muestra tres gráficos de líneas independientes con varias series de una consulta de registro en un periodo. |

## <a name="list-of-queries-part"></a>Elemento Lista de consultas
Muestra una lista de las consultas de búsqueda de registros.  Hola usuario puede hacer clic en cada consulta toodisplay sus resultados.  vista de Hello incluirá una única consulta de forma predeterminada, y puede hacer clic en **+ consulta** consultas adicionales de tooadd.

![Vista Lista de consultas](media/log-analytics-view-designer/view-list-queries.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título |Texto toodisplay princip Hola de vista de Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Filtros previamente seleccionados |Lista delimitada por comas de propiedades tooinclude en panel de filtro izquierdo de hello cuando el usuario de hello selecciona una consulta. |
| Modo de representación |Vista inicial que se muestra cuando se selecciona la consulta de Hola.  usuario de Hello puede seleccionar todas las vistas disponibles después de abrir consulta Hola. |
| **Consultas** | |
| Consulta de búsqueda |Toorun de consulta. |
| Nombre descriptivo |Nombre descriptivo de hello consultar toodisplay toohello el usuario. |

## <a name="number--list-part"></a>Elemento Number & list (Número y lista)
El encabezado tiene un solo número que muestra la cantidad de registros de una consulta de búsqueda de registros.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo.

![Vista Lista de consultas](media/log-analytics-view-designer/view-number-list.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Texto toodisplay princip Hola de vista de Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| Usar icono |Seleccione la presentación del icono toohave Hola. |
| **Título** | |
| Leyenda |Texto toodisplay princip Hola del encabezado de Hola. |
| Consultar |Toorun de consulta para el encabezado de Hola.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| **Lista** | |
| Consultar |Toorun de consulta de lista de Hola.  Hola primeras dos propiedades para hello diez primeros registros en los resultados de Hola se mostrarán.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Las barras se crean automáticamente en función de valor relativo de Hola de columna numérica Hola.<br><br>Use el comando de ordenación de hello en registros de hello toosort hello las consultas en la lista de Hola.  puede hacer clic en el usuario de Hello vea todos los hello toorun consultar y devolver todos los registros. |
| Hide graph (Ocultar gráfico) |Seleccione toodisable Hola gráfico toohello derecha de la columna numérica Hola. |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Color |Color de las barras de Hola o minigráficos. |
| Name & Value Separator (Separador de nombre y valor) |Delimitador de carácter único si desea text (propiedad) tooparse hello en varios valores.  Consulte [Configuración común](#name-value-separator) para obtener más información. |
| Consulta de navegación |Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Consulte [Configuración común](#navigation-query) para obtener más información. |
| **Lista** |**&gt; Títulos de columna** |
| Nombre |Texto toodisplay en parte superior de hello de la primera columna de la lista de Hola de Hola. |
| Valor |Texto toodisplay en parte superior de saludo de la segunda columna de la lista de Hola de Hola. |
| **Lista** |**&gt; Umbrales** |
| Enable Thresholds (Habilitar umbrales) |Seleccione tooenable umbrales.  Consulte [Configuración común](#thresholds) para obtener más información. |

## <a name="two-numbers--list-part"></a>Elemento Dos números y lista
El encabezado tiene dos números que muestran la cantidad de registros de consultas de búsqueda de registros independientes.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo.

![Vista Dos números y lista](media/log-analytics-view-designer/view-two-numbers-list.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Texto toodisplay princip Hola de vista de Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| Usar icono |Seleccione la presentación del icono toohave Hola. |
| **Título** | |
| Leyenda |Texto toodisplay princip Hola del encabezado de Hola. |
| Consultar |Toorun de consulta para el encabezado de Hola.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| **Lista** | |
| Consultar |Toorun de consulta de lista de Hola.  Hola primeras dos propiedades para hello diez primeros registros en los resultados de Hola se mostrarán.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Las barras se crean automáticamente en función de valor relativo de Hola de columna numérica Hola.<br><br>Use el comando de ordenación de hello en registros de hello toosort hello las consultas en la lista de Hola.  puede hacer clic en el usuario de Hello vea todos los hello toorun consultar y devolver todos los registros. |
| Hide graph (Ocultar gráfico) |Seleccione toodisable Hola gráfico toohello derecha de la columna numérica Hola. |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Color |Color de las barras de Hola o minigráficos. |
| Operación |Tooperform de operación de minigráfico de Hola.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Name & Value Separator (Separador de nombre y valor) |Delimitador de carácter único si desea text (propiedad) tooparse hello en varios valores.  Consulte [Configuración común](#name-value-separator) para obtener más información. |
| Consulta de navegación |Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Consulte [Configuración común](#navigation-query) para obtener más información. |
| **Lista** |**&gt; Títulos de columna** |
| Nombre |Texto toodisplay en parte superior de hello de la primera columna de la lista de Hola de Hola. |
| Valor |Texto toodisplay en parte superior de saludo de la segunda columna de la lista de Hola de Hola. |
| **Lista** |**&gt; Umbrales** |
| Enable Thresholds (Habilitar umbrales) |Seleccione tooenable umbrales.  Consulte [Configuración común](#thresholds) para obtener más información. |

## <a name="donut--list-part"></a>Elemento Donut & list (Anillo y lista)
El encabezado muestra un solo número resumido obtenido a partir de una columna de valor de una consulta de registros.  anillo de Hello gráficamente muestra resultados de registros de tres principales Hola.

![Vista Donut & list (Anillo y lista)](media/log-analytics-view-designer/view-donut-list.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Icono texto toodisplay princip Hola Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| Usar icono |Seleccione la presentación del icono toohave Hola. |
| **Encabezado** | |
| Título |Texto toodisplay princip Hola del encabezado de Hola. |
| Subtítulo |Texto toodisplay bajo el título arriba, Hola del encabezado de Hola Hola. |
| **Anillo** | |
| Consultar |Consultar toorun para anillos de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico. |
| **Anillo** |**&gt; Centro** |
| Texto |Toodisplay de texto en el valor dentro de anillo de Hola Hola. |
| Operación |Hola tooperform operación en un único valor de hello valor propiedad toosummarize tooa.<br><br>-Sum: Agregar valores de hello de todos los registros.<br>-Porcentaje: Porcentaje de los registros de hello devueltos por los valores de hello en **dar lugar a valores que se utilizan en el funcionamiento del centro de** toohello total de registros en la consulta de Hola. |
| Valores de resultado usados en la operación central |Opcionalmente, haga clic en Hola signo tooadd uno o varios valores.  resultados de Hola de consulta de hello serán toorecords limitado con valores de propiedad de Hola que especifique.  Si no se agrega ningún valor, todos los registros se incluyen en la consulta de Hola. |
| **Opciones adicionales** |**&gt; Colores** |
| Color 1<br>Color 2<br>Color 3 |Seleccione color Hola Hola de valores de hello mostrados en anillo de Hola. |
| **Opciones adicionales** |**&gt; Asignación de color avanzada** |
| Valor de campo |Nombre de un campo toodisplay Hola de tipo como un color diferente si se incluye en anillo de Hola. |
| Color |Seleccione color de hello para el campo único de Hola. |
| **Lista** | |
| Consultar |Toorun de consulta de lista de Hola.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| Hide graph (Ocultar gráfico) |Seleccione toodisable Hola gráfico toohello derecha de la columna numérica Hola. |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Color |Color de las barras de Hola o minigráficos. |
| Operación |Tooperform de operación de minigráfico de Hola.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Name & Value Separator (Separador de nombre y valor) |Delimitador de carácter único si desea text (propiedad) tooparse hello en varios valores.  Consulte [Configuración común](#name-value-separator) para obtener más información. |
| Consulta de navegación |Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Consulte [Configuración común](#navigation-query) para obtener más información. |
| **Lista** |**&gt; Títulos de columna** |
| Nombre |Texto toodisplay en parte superior de hello de la primera columna de la lista de Hola de Hola. |
| Valor |Texto toodisplay en parte superior de saludo de la segunda columna de la lista de Hola de Hola. |
| **Lista** |**&gt; Umbrales** |
| Enable Thresholds (Habilitar umbrales) |Seleccione tooenable umbrales.  Consulte [Configuración común](#thresholds) para obtener más información. |

## <a name="two-timelines--list-part"></a>Elemento Dos escalas de tiempo y lista
Encabezado muestra hello resultados de las consultas de dos registros con el tiempo como gráficos de columnas con una llamada de mostrar un número único de resumen a partir de una columna de valor en una consulta de registro.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo.

![Vista Dos escalas de tiempo y lista](media/log-analytics-view-designer/view-two-timelines-list.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Icono texto toodisplay princip Hola Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| Usar icono |Seleccione la presentación del icono toohave Hola. |
| **Primer gráfico<br>Segundo gráfico** | |
| Leyenda |Toodisplay de texto en la llamada de hello para la primera serie de Hola. |
| Color |Toouse de color para las columnas de hello en serie de Hola. |
| Consultar |Toorun de consulta para la primera serie de Hola.  recuento de Hello del número de Hola de registros en cada intervalo de tiempo se representará mediante columnas de gráfico de Hola. |
| Operación |Hola tooperform operación en hello valor toosummarize tooa único valor de propiedad para la llamada de Hola.<br><br>-Sum: Suma del valor de Hola de todos los registros.<br>-Promedio: El promedio del valor de Hola de todos los registros.<br>-Último ejemplo: El valor del último intervalo de hello incluido en el gráfico de Hola.<br>-Primer ejemplo: El valor del primer intervalo de hello incluido en el gráfico de Hola.<br>-Recuento: El recuento de todos los registros devueltos por la consulta de Hola. |
| **Lista** | |
| Consultar |Toorun de consulta de lista de Hola.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| Hide graph (Ocultar gráfico) |Seleccione toodisable Hola gráfico toohello derecha de la columna numérica Hola. |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Color |Color de las barras de Hola o minigráficos. |
| Operación |Tooperform de operación de minigráfico de Hola.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Consulta de navegación |Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Consulte [Configuración común](#navigation-query) para obtener más información. |
| **Lista** |**&gt; Títulos de columna** |
| Nombre |Texto toodisplay en parte superior de hello de la primera columna de la lista de Hola de Hola. |
| Valor |Texto toodisplay en parte superior de saludo de la segunda columna de la lista de Hola de Hola. |
| **Lista** |**&gt; Umbrales** |
| Enable Thresholds (Habilitar umbrales) |Seleccione tooenable umbrales.  Consulte [Configuración común](#thresholds) para obtener más información. |

## <a name="information-part"></a>Elemento Información
El encabezado muestra texto estático y un vínculo opcional.  La lista muestra uno o varios elementos con texto estático y un título.

![Vista Información](media/log-analytics-view-designer/view-information.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Icono texto toodisplay princip Hola Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Color |Color de fondo de encabezado de Hola. |
| **Encabezado** | |
| Imagen |Toodisplay de archivo de imagen en el encabezado de Hola. |
| Etiqueta |Toodisplay de texto en el encabezado de Hola. |
| **Encabezado** |**&gt; Vínculo** |
| Etiqueta |Texto del vínculo. |
| URL |Dirección URL del vínculo. |
| **Elementos de información** | |
| Título |Toodisplay de texto de título de cada elemento. |
| Contenido |Toodisplay de texto para cada elemento. |

## <a name="line-chart-callout--list-part"></a>Elemento Gráfico de líneas, llamada, lista
El encabezado muestra un gráfico de líneas con varias series de una consulta de registro en un periodo y una llamada con un valor resumido.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo.

![Vista Gráfico de líneas, llamada, lista](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Icono texto toodisplay princip Hola Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| Usar icono |Seleccione la presentación del icono toohave Hola. |
| **Encabezado** | |
| Título |Texto toodisplay princip Hola del encabezado de Hola. |
| Subtítulo |Texto toodisplay bajo el título arriba, Hola del encabezado de Hola Hola. |
| **Gráfico de líneas** | |
| Consultar |Toorun de consulta para el gráfico de líneas de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Esto suele ser una consulta que utiliza hello **medida** resultados de toosummarize de palabra clave.  Si la consulta de hello utiliza hello **intervalo** (palabra clave), a continuación, Hola eje x del gráfico de hello usará este intervalo de tiempo.  Si consulta hello no incluye hello **intervalo** intervalos de palabra clave, a continuación, cada hora se usan para saludo del eje x. |
| **Gráfico de líneas** |**&gt; Llamada** |
| Título de la llamada |Texto toodisplay por encima del valor de la llamada de Hola. |
| Nombre de la serie |Valor de propiedad para toouse de serie de hello para el valor de la llamada de Hola.  Si no se proporciona ninguna serie, se utilizan todos los registros de consulta de Hola. |
| Operación |Hola tooperform operación en hello valor toosummarize tooa único valor de propiedad para la llamada de Hola.<br><br>-Promedio: El promedio del valor de Hola de todos los registros.<br>-Recuento de todos los registros devueltos por la consulta de Hola.<br>-Último ejemplo: El valor del último intervalo de hello incluido en el gráfico de Hola.<br>-Max: Valor de máximo uno de los intervalos de hello incluidos en el gráfico de Hola.<br>-Mínimo: Valor mínimo uno de los intervalos de hello incluidos en el gráfico de Hola.<br>-Sum: Suma del valor de Hola de todos los registros. |
| **Gráfico de líneas** |**&gt; Eje Y** |
| Usar escala logarítmica |Seleccione toouse una escala logarítmica para hello eje y. |
| Unidades |Especifique unidades de Hola para los valores de hello devueltos por la consulta de Hola.  Esta información es toodisplay usa etiquetas en el gráfico de Hola que indica los tipos de valor de hello y, opcionalmente, para convertir los valores de hello.  Hola tipo de unidad especifica la categoría de Hola de unidad de Hola y define los valores de tipo de unidad actual de Hola que están disponibles.  Si selecciona un valor numérico de Convert toothen Hola se convierten valores de hello unidad actual tipo toohello Convert tootype. |
| Etiqueta personalizada |Texto toodisplay para hello Y siguiente toohello etiqueta de eje para el tipo de unidad de Hola.  Si no se especifica ninguna etiqueta, se muestra sólo el tipo de unidad Hola. |
| **Lista** | |
| Consultar |Toorun de consulta de lista de Hola.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| Hide graph (Ocultar gráfico) |Seleccione toodisable Hola gráfico toohello derecha de la columna numérica Hola. |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Color |Color de las barras de Hola o minigráficos. |
| Operación |Tooperform de operación de minigráfico de Hola.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Name & Value Separator (Separador de nombre y valor) |Delimitador de carácter único si desea text (propiedad) tooparse hello en varios valores.  Consulte [Configuración común](#name-value-separator) para obtener más información. |
| Consulta de navegación |Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Consulte [Configuración común](#navigation-query) para obtener más información. |
| **Lista** |**&gt; Títulos de columna** |
| Nombre |Texto toodisplay en parte superior de hello de la primera columna de la lista de Hola de Hola. |
| Valor |Texto toodisplay en parte superior de saludo de la segunda columna de la lista de Hola de Hola. |
| **Lista** |**&gt; Umbrales** |
| Enable Thresholds (Habilitar umbrales) |Seleccione tooenable umbrales.  Consulte [Configuración común](#thresholds) para obtener más información. |

## <a name="line-chart--list-part"></a>Elemento gráfico de líneas y lista
El encabezado muestra un gráfico de líneas con varias series de una consulta de registro en un periodo.  Lista muestra hello diez primeros resultados de una consulta con un gráfico que indica el valor relativo de Hola de una columna numérica o sus cambios con el tiempo.

![Vista Gráfico de líneas y lista](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Icono texto toodisplay princip Hola Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| Usar icono |Seleccione la presentación del icono toohave Hola. |
| **Encabezado** | |
| Título |Texto toodisplay princip Hola del encabezado de Hola. |
| Subtítulo |Texto toodisplay bajo el título arriba, Hola del encabezado de Hola Hola. |
| **Gráfico de líneas** | |
| Consultar |Toorun de consulta para el gráfico de líneas de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Esto suele ser una consulta que utiliza hello **medida** resultados de toosummarize de palabra clave.  Si la consulta de hello utiliza hello **intervalo** (palabra clave), a continuación, Hola eje x del gráfico de hello usará este intervalo de tiempo.  Si consulta hello no incluye hello **intervalo** intervalos de palabra clave, a continuación, cada hora se usan para saludo del eje x. |
| **Gráfico de líneas** |**&gt; Eje Y** |
| Usar escala logarítmica |Seleccione toouse una escala logarítmica para hello eje y. |
| Unidades |Especifique unidades de Hola para los valores de hello devueltos por la consulta de Hola.  Esta información es toodisplay usa etiquetas en el gráfico de Hola que indica los tipos de valor de hello y, opcionalmente, para convertir los valores de hello.  Hola tipo de unidad especifica la categoría de Hola de unidad de Hola y define los valores de tipo de unidad actual de Hola que están disponibles.  Si selecciona un valor numérico de Convert toothen Hola se convierten valores de hello unidad actual tipo toohello Convert tootype. |
| Etiqueta personalizada |Texto toodisplay para hello Y siguiente toohello etiqueta de eje para el tipo de unidad de Hola.  Si no se especifica ninguna etiqueta, se muestra sólo el tipo de unidad Hola. |
| **Lista** | |
| Consultar |Toorun de consulta de lista de Hola.  se mostrará el recuento de Hello del número de Hola de registros devueltos por la consulta de Hola. |
| Hide graph (Ocultar gráfico) |Seleccione toodisable Hola gráfico toohello derecha de la columna numérica Hola. |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Color |Color de las barras de Hola o minigráficos. |
| Operación |Tooperform de operación de minigráfico de Hola.  Consulte [Configuración común](#sparklines) para obtener más información. |
| Name & Value Separator (Separador de nombre y valor) |Delimitador de carácter único si desea text (propiedad) tooparse hello en varios valores.  Consulte [Configuración común](#name-value-separator) para obtener más información. |
| Consulta de navegación |Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Consulte [Configuración común](#navigation-query) para obtener más información. |
| **Lista** |**&gt; Títulos de columna** |
| Nombre |Texto toodisplay en parte superior de hello de la primera columna de la lista de Hola de Hola. |
| Valor |Texto toodisplay en parte superior de saludo de la segunda columna de la lista de Hola de Hola. |
| **Lista** |**&gt; Umbrales** |
| Enable Thresholds (Habilitar umbrales) |Seleccione tooenable umbrales.  Consulte [Configuración común](#thresholds) para obtener más información. |

## <a name="stack-of-line-charts-part"></a>Elemento Stack of line charts (Pila de gráficos de líneas)
Muestra tres gráficos de líneas independientes con varias series de una consulta de registro en un periodo.

![Stack of line charts (Pila de gráficos de líneas)](media/log-analytics-view-designer/view-stack-line-charts.png)

| Configuración | Descripción |
|:--- |:--- |
| **General** | |
| Título de grupo |Icono texto toodisplay princip Hola Hola. |
| Nuevo grupo |Seleccione toocreate un nuevo grupo en la vista de Hola a partir de la vista actual de Hola. |
| Icono |Imagen archivo toodisplay toohello resultado siguiente en el encabezado de Hola. |
| **Gráfico 1<br>Gráfico 2<br>Gráfico 3** |**&gt; Encabezado** |
| Título |Texto toodisplay en parte superior de hello del gráfico de Hola. |
| Subtítulo |Toodisplay de texto en el título a la parte superior de hello del gráfico de Hola Hola. |
| **Gráfico 1<br>Gráfico 2<br>Gráfico 3** |**Gráfico de líneas** |
| Consultar |Toorun de consulta para el gráfico de líneas de Hola.  la propiedad first Hola debe ser un texto hello y valor segunda propiedad un valor numérico.  Esto suele ser una consulta que utiliza hello **medida** resultados de toosummarize de palabra clave.  Si la consulta de hello utiliza hello **intervalo** (palabra clave), a continuación, Hola eje x del gráfico de hello usará este intervalo de tiempo.  Si consulta hello no incluye hello **intervalo** intervalos de palabra clave, a continuación, cada hora se usan para saludo del eje x. |
| **Gráfico** |**&gt; Eje Y** |
| Usar escala logarítmica |Seleccione toouse una escala logarítmica para hello eje y. |
| Unidades |Especifique unidades de Hola para los valores de hello devueltos por la consulta de Hola.  Esta información es toodisplay usa etiquetas en el gráfico de Hola que indica los tipos de valor de hello y, opcionalmente, para convertir los valores de hello.  Hola tipo de unidad especifica la categoría de Hola de unidad de Hola y define los valores de tipo de unidad actual de Hola que están disponibles.  Si selecciona un valor numérico de Convert toothen Hola se convierten valores de hello unidad actual tipo toohello Convert tootype. |
| Etiqueta personalizada |Texto toodisplay para hello Y siguiente toohello etiqueta de eje para el tipo de unidad de Hola.  Si no se especifica ninguna etiqueta, se muestra sólo el tipo de unidad Hola. |

## <a name="common-settings"></a>Configuración común
Hola siguientes secciones describe los elementos de visualización de tooseveral comunes de configuración.

### <a name="name-value-separator">Name &amp; Value Separator</a> (Separador de nombre y valor)
Delimitador de carácter único si desea propiedad de texto de hello tooparse desde una consulta de lista en varios valores.  Si especifica un delimitador, se pueden proporcionar los nombres de cada campo separadas por hello mismo delimitador en el cuadro de nombre de Hola.

Por ejemplo, una propiedad llamada "*location*" que incluya valores como *Redmond-Building41* y *Bellevue-Building12*.  Puede especificar – para hello nombre & separador Value y *City Building* para hello nombre.  De este modo, se analizaría cada valor en dos propiedades denominadas "*City*" y "*Building*".

### <a name="navigation-query">Consulta de navegación</a>
Una consulta toorun al usuario Hola selecciona un elemento de lista de Hola.  Use *{elemento seleccionado}* tooinclude sintaxis Hola elemento que Hola seleccionado por el usuario.

Por ejemplo, si hello consulta tiene una columna llamada *equipo* y consulta de navegación de hello es *{elemento seleccionado}*, una consulta como *equipo = "MyComputer"* se ejecutaría cuando usuario de Hello había seleccionado un equipo.  Si consulta de navegación de hello es *tipo = evento {elemento seleccionado}* , a continuación, consulta de hello *tipo = evento Computer = "MyComputer"* se ejecutaría.

### <a name="sparklines">Minigráficos</a>
Un minigráfico es un gráfico de líneas pequeño que se muestra el valor de Hola de una entrada de lista con el tiempo.  Para las partes de la visualización con una lista, puede seleccionar si toodisplay una barra horizontal que indique Hola valor relativo de una columna numérica o un minigráfico que indica su valor con el tiempo.

Hello en la tabla siguiente describe la configuración de Hola de los minigráficos.

| Configuración | Descripción |
|:--- |:--- |
| Enable sparklines (Habilitar los minigráficos) |Seleccione minigráfico toodisplay en lugar de la barra horizontal. |
| Operación |Si se habilitan los minigráficos, esto es tooperform de operación de hello en todas las propiedades en hello toocalculate Hola valores de lista del minigráfico Hola.<br><br>-Último ejemplo: Último valor de serie de hello en intervalo de tiempo de Hola.<br>-Máximo: Valor máximo serie de hello en intervalo de tiempo de Hola.<br>-Mínimo: Valor mínimo serie de hello en intervalo de tiempo de Hola.<br>-Sum: Suma de valores para series de hello en intervalo de tiempo de Hola.<br>-Summary: Usa Hola mismo comando de medida como consulta de hello en el encabezado de Hola. |

### <a name="thresholds">Umbrales</a>
Umbrales permiten toodisplay un elemento tooeach siguiente de icono de color en una lista que proporciona un indicador visual rápido de elementos que superen un determinado valor o se encuentren dentro de un intervalo determinado.  Por ejemplo, podría mostrar un icono verde para los elementos con un valor aceptable, amarillo si el valor de hello está dentro del intervalo que indica una advertencia y rojo si supera un valor de error.

Al habilitar umbrales en un elemento, debe especificar uno o varios umbrales.  Si el valor de Hola de un elemento es mayor que un valor de umbral e inferior al valor de umbral de hello siguiente, se utiliza ese color.  Si el elemento de hello es mayor que, a continuación, mayor valor de umbral, se establece ese color.   

Cada conjunto de umbral tiene un umbral con un valor de **Predeterminado**.  Se trata de establecer si no se supera ningún otro valor de color de Hola.  Puede agregar o quitar umbrales haciendo clic en hello  **+**  o **x** botón.

Hello en la tabla siguiente describe la configuración de Hola de límites.

| Configuración | Description |
|:--- |:--- |
| Enable Thresholds (Habilitar umbrales) |Seleccione toodisplay que un toohello de icono de color a la izquierda de cada valor que indica sus umbrales toospecified relativa de mantenimiento. |
| Nombre |Valor de umbral de nombre tooidentify Hola. |
| Umbral |Valor de umbral de Hola.  color de estado de Hola para cada elemento de lista se establece toohello color hello más alto de valor de umbral superado por el valor del elemento de Hola.  No hay un umbral predeterminado que es el color de hello si no hay valores de umbral se supera. |
| Color |Color para valor de umbral de Hola. |

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) toosupport consultas de hello en partes de visualización.
