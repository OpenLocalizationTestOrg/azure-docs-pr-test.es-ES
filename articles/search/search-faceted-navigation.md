---
title: "aaaHow tooimplement la navegación por facetas en búsqueda de Azure | Documentos de Microsoft"
description: "Agregar tooapplications de navegación por facetas que se integran con búsqueda de Azure, un servicio de búsqueda en la nube hospedado en Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>¿Cómo tooimplement la navegación por facetas en búsqueda de Azure
La navegación por facetas es un mecanismo de filtrado que proporciona una navegación en profundidad autodirigida en aplicaciones de búsqueda. término de Hello 'navegación por facetas' puede ser desconocida, pero probablemente ha usado con anterioridad. Como Hola siguiente ejemplo se muestra la navegación por facetas es nada más que Hola categorías utilizadas toofilter resultados.

 ![Azure Search Job Portal Demo (Demostración del portal de búsqueda de trabajo de Azure Search)][1]

Navegación por facetas es un toosearch de punto de entrada alternativo. Ofrece una cómoda tootyping alternativo expresiones de búsqueda compleja a mano. Las facetas pueden ayudarle a encontrar lo que busca y le garantizan que obtendrá al menos un resultado. Como desarrollador, facetas le permiten exponer los criterios de búsqueda más útiles de Hola para navegar por el corpus de búsqueda. En las aplicaciones de tienda en línea, la navegación por facetas suele basarse en marcas, departamentos (zapatos para niños), tamaño, precio, popularidad y clasificación. 

La implementación de la navegación por facetas difiere en las distintas tecnologías de búsqueda. En Azure Search, la navegación por facetas se compila en tiempo de consulta usando campos que haya atribuido anteriormente en el esquema.

-   En las consultas de Hola que la aplicación se compila, debe enviar una consulta *parámetros de consulta de faceta* tooget Hola disponible filtro los valores de facetas para ese documento en el conjunto de resultados.

-   tooactually recortar el conjunto de resultados de documento de hello, también debe aplicar la aplicación hello un `$filter` expresión.

En el desarrollo de aplicaciones, escribir código que construye consultas constituye masiva Hola de trabajo de Hola. Muchos de los comportamientos de aplicación Hola que se esperaría de navegación por facetas se proporcionan con el servicio de hello, incluida la compatibilidad integrada para definir intervalos y obtener recuentos de resultados de la faceta. servicio de Hello también incluye valores predeterminados razonables que le ayudarán a evitar las estructuras de navegación difícil de manejar. 

## <a name="sample-code-and-demo"></a>Demostración y código de ejemplo
En este artículo se utiliza como ejemplo un portal de búsqueda de trabajo. ejemplo de Hola se implementa como una aplicación ASP.NET MVC.

-   Ver y probar demostración en línea de hello trabajar en [demostración de Portal de trabajo de búsqueda de Azure](http://azjobsdemo.azurewebsites.net/).

-   Descargar código de hello de hello [repositorio de ejemplos de Azure en GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>Primeros pasos
Si es nuevo desarrollo toosearch, hello toothink de manera mejor de navegación por facetas es que muestra las posibilidades de hello para la búsqueda autodirigido. Es un tipo de experiencia de búsqueda en profundidad basada en filtros predefinidos, que se usa para restringir rápidamente los resultados de búsqueda mediante acciones de apuntar y hacer clic. 

### <a name="interaction-model"></a>Modelo de interacción

experiencia de búsqueda de Hello para la navegación por facetas es iterativa, así que vamos a conocer como una secuencia de las consultas que expandir en las acciones de respuesta toouser.

Hola punto inicial es una página de aplicación que permite la navegación por facetas, que normalmente se colocan en la periferia de Hola. La navegación por facetas suele tener una estructura de árbol con casillas para cada valor o texto en el que se puede hacer clic. 

1. Una consulta enviada tooAzure búsqueda especifica la estructura de navegación por facetas de Hola a través de uno o más parámetros de consulta de faceta. Por ejemplo, pueden incluir consultas de hello `facet=Rating`, quizás con una `:values` o `:sort` toofurther opción Refinar la presentación de Hola.
2. capa de presentación de Hello presenta una página de búsqueda que permite la navegación por facetas, con facetas de hello especificadas en la solicitud de saludo.
3. Proporciona una estructura de navegación por facetas que incluye clasificación, hacer clic en "4" tooindicate que se deben mostrar solo los productos con una clasificación de 4 o posterior. 
4. En respuesta, la aplicación hello envía una consulta que incluye`$filter=Rating ge 4` 
5. Hola presentación capa Hola página actualizaciones, que muestra un conjunto de resultados reducido que contiene únicamente los elementos que satisfacen los criterios de hello nuevo (en este caso, productos clasifican 4 y superiores).

Una faceta es un parámetro de consulta, pero no lo confunda con una entrada de consulta. Nunca se usa como criterio de selección en una consulta. En su lugar, cree faceta parámetros de consulta como la estructura de navegación de toohello de entradas que se devolverán en respuesta de Hola. Para cada parámetro de consulta de faceta que proporcione, búsqueda de Azure se evalúa como cuántos documentos se encuentran en los resultados parciales Hola para cada valor de faceta.

Hola aviso `$filter` en el paso 4. filtro de Hello es un aspecto importante de la navegación por facetas. Aunque las facetas y los filtros son independientes en hello API, debe ambos experiencia de hello toodeliver piensa. 

### <a name="app-design-pattern"></a>Patrón de diseño de la aplicación

En código de aplicación, el patrón de Hola es el estructura de navegación por facetas de toouse faceta consulta parámetros tooreturn Hola junto con los resultados de faceta, además de una expresión de $filter.  click (evento) en el valor de la faceta de Hola Hola Hola de identificadores de expresión de filtro. Reflexión de hello `$filter` expresión como código de hello detrás de recorte de hello real de los resultados de la búsqueda devolvió toohello capa de presentación. Dada una faceta de colores, haga clic en color rojo de Hola se implementa a través de un `$filter` expresión que selecciona solo aquellos elementos que tienen un color rojo. 

### <a name="query-basics"></a>Conceptos básicos de las consultas

En Búsqueda de Azure, una solicitud se especifica mediante uno o más parámetros de consulta (consulte [Buscar documentos](http://msdn.microsoft.com/library/azure/dn798927.aspx) para obtener una descripción de cada uno). Ninguno de los parámetros de consulta de hello son necesaria, pero debe tener al menos una en orden para un toobe de consulta válida.

Precisión, comprendido toofilter capacidad out aciertos irrelevantes, hello se logra una a través de una o ambas de estas expresiones:

-   **search=**  
    valor de Hola de este parámetro constituye la expresión de búsqueda de Hola. Podría ser un fragmento de texto o una expresión de búsqueda compleja que incluye varios términos y operadores. En el servidor de hello, una expresión de búsqueda se utiliza para la búsqueda de texto completo, consultar los campos de búsqueda en índice hello para la coincidencia de términos, devolver los resultados en orden de rango. Si establece `search` toonull, ejecución de la consulta es sobre todo índice de hello (es decir, `search=*`). In this Case, consultar otros elementos de hello, como un `$filter` o perfil de puntuación, es Hola principales factores que afectan a los documentos que se devuelven `($filter`) y en qué orden (`scoringProfile` o `$orderby`).

-   **$filter=**  
    Un filtro es un mecanismo eficaz para limitar el tamaño de Hola de resultados de la búsqueda en función de los valores de hello de atributos de documento específico. Un `$filter` se evalúa en primer lugar, seguida de lógica de facetas que genera valores disponibles de Hola y el número correspondiente para cada valor

Expresiones de búsqueda compleja disminuir el rendimiento de Hola de consulta de Hola. Siempre que sea posible, utilice la precisión de tooincrease de expresiones de filtro bien construido y mejorar el rendimiento de las consultas.

toobetter comprender cómo agrega un filtro con mayor precisión, comparar un tooone de expresión de búsqueda compleja que incluye una expresión de filtro:

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Ambas consultas son válidos, pero hello en segundo lugar es la mejor opción si está buscando no moteles con estacionamiento en Seattle.
-   consulta primera Hola se basa en esas palabras específicas que se menciona o no se menciona en los campos de cadena como nombre, descripción y cualquier otro campo que contiene datos de búsqueda.
-   segunda consulta de Hola busca coincidencias precisas en los datos estructurados y es probable que toobe mucho más precisa.

En las aplicaciones que incluyen navegación por facetas, asegúrese de que cada acción del usuario en una estructura de navegación por facetas vaya acompañada de una restricción de los resultados de búsqueda. resultados de toonarrow, utilice una expresión de filtro.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Compilación de una aplicación de navegación por facetas
Implementar la navegación por facetas con búsqueda de Azure en el código de aplicación que se basa la solicitud de búsqueda de Hola. navegación por facetas Hola se basa en elementos del esquema que definió anteriormente.

Predefinidas en el índice de búsqueda es hello `Facetable [true|false]` atributo de índice, establecer en los campos seleccionados tooenable o deshabilitar su uso en una estructura de navegación por facetas. Sin `"Facetable" = true`, un campo no se puede usar en la navegación por facetas.

capa de presentación de Hello en el código proporciona la experiencia del usuario Hola. Deben enumerar elementos que componen Hola la navegación por facetas hello, como etiqueta de hello, valores, casillas y recuento de Hola. Hola API de REST de búsqueda de Azure es independiente de la plataforma, así que usa el idioma y la plataforma que desee. Hola importante que es tooinclude elementos de interfaz de usuario que admiten incremental actualización, con el estado actualizado de interfaz de usuario que se ha seleccionado cada faceta adicional. 

En el momento de la consulta, el código de aplicación crea una solicitud que incluye `facet=[string]`, un parámetro de solicitud que proporciona Hola campo toofacet por. Una consulta puede tener varias facetas, como `&facet=color&facet=category&facet=rating`, separadas por un carácter de y comercial (&).

Código de la aplicación también debe construir un `$filter` hello toohandle de expresión, haga clic en los eventos de navegación por facetas. Un `$filter` reduce los resultados de búsqueda de hello, utilice el valor de la faceta de Hola como criterios de filtro.

Búsqueda de Azure devuelve los resultados de búsqueda de hello, en función de uno o más términos que escriba, junto con la estructura de navegación por facetas de toohello de actualizaciones. En Búsqueda de Azure, la navegación por facetas es una construcción de un solo nivel, con los valores de las facetas y los recuentos de cuántos resultados se encuentran para cada una.

En las secciones siguientes de hello, tomamos un vistazo más de cerca a cómo toobuild cada parte.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Generar índice Hola
Facetas de está habilitada de forma de campo a campo en el índice de hello, a través de este atributo de índice: `"Facetable": true`.  
Todos los tipos de campo que podrían usarse en la navegación por facetas son `Facetable` de forma predeterminada. Estos tipos de campo incluyen `Edm.String`, `Edm.DateTimeOffset`, y todos los campos de tipo numérico de Hola (básicamente, todos los tipos de campo son facetable excepto `Edm.GeographyPoint`, que no se puede usar en la navegación por facetas). 

Cuando se crea un índice, una práctica recomendada para la navegación por facetas está tooexplicitly activar facetas desactivada para los campos que nunca deben utilizarse como una faceta.  En concreto, los campos de cadena para los valores de singleton, por ejemplo, un identificador o nombre del producto, deben estar definidos demasiado`"Facetable": false` tooprevent sus accidental (e ineficaces) se utilizan en la navegación por facetas. Facetas desactivar donde no es necesario la activación ayuda a mantener pequeño tamaño Hola de índice de Hola y suele mejora el rendimiento.

Aquí te mostramos parte del esquema de hello para la aplicación de ejemplo de Hola demostración de Portal de trabajo, quitar de un determinado tamaño atributos tooreduce hello:

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Como puede ver en el esquema de ejemplo Hola `Facetable` se ha desactivado para los campos de cadena que no deben usarse como facetas, como los valores de identificador. Facetas desactivar donde no es necesario la activación ayuda a mantener pequeño tamaño Hola de índice de Hola y suele mejora el rendimiento.

> [!TIP]
> Como práctica recomendada, incluyen el conjunto completo de Hola de atributos de índice para cada campo. Aunque `Facetable` está de forma predeterminada para casi todos los campos, establecer deliberadamente cada atributo puede ayudarle a considerar detenidamente las implicaciones de Hola de cada decisión de esquema. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Comprobar los datos de Hola
calidad de Hola de los datos tiene un efecto directo en si la estructura de navegación por facetas de hello materializa tal y como se espera que. También afecta a la facilidad de Hola de construir el conjunto de resultados de filtros tooreduce Hola.

Si desea toofacet por marca o precio, cada documento debe contener valores de *marca* y *ProductPrice* que son válidos, coherentes y productivos como una opción de filtro.

Estos son algunos avisos de qué tooscrub para:

* Para cada campo que desee toofacet por, pregúntese si contiene valores que son adecuados como filtros en la búsqueda autodirigido. valores de Hello deben ser suficientemente distintiva, corto y descriptivo toooffer una opción clara entre las opciones de la competencia.
* Errores ortográficos o valores casi coincidentes. Si faceta en Color y los valores de campo incluyen naranja y Ornage (una palabra mal escrita), una faceta basada en el campo de Color Hola seleccionará ambos.
* La mezcla de mayúsculas y minúsculas en el texto también puede causar estragos en la navegación por facetas, porque naranja y Naranja aparecen como dos valores diferentes. 
* Versiones simples y plurales de Hola mismo valor puede dar lugar a una faceta independiente para cada uno de ellos.

Como puede imaginar, diligencia en la preparación de datos de hello es un aspecto fundamental de la navegación por facetas efectivo.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Compilar Hola interfaz de usuario
Trabajar desde el nivel de presentación de hello puede descubrir los requisitos que podrían faltar en caso contrario y entender qué capacidades están toohello esencial de ayuda experiencia de búsqueda.

En cuanto a la navegación por facetas, la página web o una aplicación muestra la estructura de navegación por facetas de hello, detecta proporcionados por el usuario en la página de Hola e inserta elementos Hola cambiado. 

Para aplicaciones web, AJAX normalmente se utiliza en la capa de presentación de hello porque permite toorefresh los cambios incrementales. También puede usar ASP.NET MVC o cualquier otra plataforma de visualización que se puede conectar tooan servicio Búsqueda de Azure a través de HTTP. aplicación de ejemplo de Hola al que hace referencia a lo largo de este artículo: hello **demostración de Portal de trabajo de búsqueda de Azure** – ocurre toobe una aplicación ASP.NET MVC.

En el ejemplo de Hola, la navegación por facetas se integra en la página de resultados de búsqueda de Hola. Hola siguiente ejemplo, tomado de Hola `index.cshtml` página de resultados del archivo de aplicación de ejemplo de Hola, estructura HTML muestra hello estática para mostrar la navegación por facetas en búsqueda de Hola. lista de Hola de facetas compilarse o vuelven a generar dinámicamente cuando se envíe un término de búsqueda, o activar o desactiva una faceta.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Hola siguiente fragmento de código de hello `index.cshtml` página Hola HTML toodisplay Hola primera faceta título empresarial crea de forma dinámica. Funciones similares compilación dinámicamente hello HTML para hello otras facetas. Cada faceta tiene una etiqueta y un recuento, que muestra el número de Hola de elementos encontrados para ese resultado de la faceta.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Cuando se diseña la página de resultados de búsqueda de hello, recuerde tooadd un mecanismo para borrar las facetas. Si agrega casillas de verificación, puede ver fácilmente cómo se filtra tooclear Hola. En otros diseños, puede que necesite un patrón de ruta de navegación u otro enfoque creativo. Por ejemplo, en la aplicación de ejemplo de Portal de la búsqueda de trabajo hello, puede hacer clic en hello `[X]` después de una faceta de hello tooclear faceta seleccionada.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Crear consulta de Hola
código de Hello creado por usted para la creación de consultas debe especificar todas las partes de una consulta válida, incluyendo expresiones de búsqueda, las facetas, filtros, puntuación perfiles – nada usan tooformulate una solicitud. En esta sección, exploramos donde facetas caben en una consulta y cómo se utilizan filtros con facetas toodeliver un reducido conjunto de resultados.

Observe que las facetas son una parte integral de esta aplicación de ejemplo. experiencia de búsqueda de Hola Hola demostración de Portal de trabajo está diseñado basándose en filtros y la navegación por facetas. un lugar destacado de navegación por facetas en página Hola Hola muestra su importancia. 

Un ejemplo suele ser un buen lugar toobegin. Hola siguiente ejemplo, tomado de Hola `JobsSearch.cs` archivo, compilaciones, en función de una solicitud que crea la navegación de faceta en título empresarial, la ubicación, tipo de registro y salario mínimo. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Un parámetro de consulta de faceta se establece el campo tooa y según el tipo de datos de hello, pueden tener parámetros aún más por lista delimitada por comas que incluye `count:<integer>`, `sort:<>`, `interval:<integer>`, y `values:<list>`. Se admiten listas de valores para datos numéricos cuando se establecen intervalos. Consulte [Buscar documentos (API de Búsqueda de Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) para obtener más información sobre su uso.

Junto con las facetas, solicitud de hello formulada la aplicación debe compilarse también filtros toonarrow hacia abajo el conjunto de Hola de documentos candidatos basado en una selección de valor de faceta. Para una tienda de bicicletas, la navegación por facetas proporciona pistas tooquestions como *los colores, los fabricantes y tipos de bicicletas están disponibles?*. El filtrado responde a preguntas como *¿qué bicicletas exactas son rojas, bicicletas de montaña, dentro de este precio de intervalo de precios?*. Al hacer clic en "Rojo" tooindicate que se deben mostrar solo los productos de color rojo, aplicación de hello siguiente consulta Hola envía incluye `$filter=Color eq ‘Red’`.

Hola siguiente fragmento de código de hello `JobsSearch.cs` página agrega Hola seleccionado título empresarial toohello filtro si selecciona un valor de faceta de hello título empresarial.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>Sugerencias y procedimientos recomendados

### <a name="indexing-tips"></a>Sugerencias de indexación
**Mejora de la eficacia del índice si no utiliza un cuadro de búsqueda**

Si la aplicación utiliza la navegación por facetas exclusivamente (es decir, ningún cuadro de búsqueda), puede marcar campo hello como `searchable=false`, `facetable=true` tooproduce un índice más compacto. Además, la indización se produce solo en los valores de facetas todo, con ninguna división de palabras o una indización de componentes de Hola de un valor de múltiples palabra.

**Especificación de qué campos se pueden usar como facetas**

Recuerde que Hola esquema de índice Hola determina qué campos están disponible toouse como una faceta. Suponiendo que un campo facetable, consulta Hola especifica qué toofacet campos por. campo Hello mediante el cual está facetas proporciona valores de hello que aparecen debajo de la etiqueta de Hola. 

los valores de Hello que aparecen debajo de cada etiqueta se recuperan del índice de Hola. Por ejemplo, si hello campo de faceta es *Color*, valores de hello disponibles para realizar un filtrado adicional son valores de hello para ese campo - rojo, negro y así sucesivamente.

Para los valores de numéricos y de fecha y hora solo, puede establecer explícitamente los valores en el campo de faceta de hello (por ejemplo, `facet=Rating,values:1|2|3|4|5`). Se permite una lista de valores para estos tipos toosimplify Hola separación de campos de resultados de faceta en intervalos contiguos (ya sea intervalos basados en valores numéricos o períodos de tiempo). 

**De forma predeterminada solo puede tener un nivel de navegación por facetas** 

Como ya se mencionó, no hay compatibilidad directa para facetas anidadas en una jerarquía. De forma predeterminada, la navegación por facetas en Azure Search solo admite un nivel de filtros. Sin embargo, existen soluciones alternativas. Puede codificar una estructura jerárquica de facetas en una `Collection(Edm.String)` con un punto de entrada por jerarquía. Implementar esta solución alternativa es más allá del ámbito de Hola de este artículo. 

### <a name="querying-tips"></a>Sugerencias de consulta
**Validar los campos**

Si compila lista Hola de facetas de manera dinámica basándose en la entrada de usuario de confianza, valide que Hola nombres de campos por facetas Hola son válidos. O bien, al generar direcciones URL mediante el uso de escape nombres Hola `Uri.EscapeDataString()` en. NET, o hello equivalente en la plataforma de elección.

### <a name="filtering-tips"></a>Sugerencias de filtrado
**Aumento de la precisión de la búsqueda con filtros**

Use filtros. Si confía en expresiones de búsqueda solo por sí sola y lematización podría provocar un toobe documento devuelven que no tiene valor de faceta precisa de hello en cualquiera de sus campos.

**Aumento del rendimiento de la búsqueda con filtros**

Filtros de restringir el conjunto de Hola de documentos de candidatos para la búsqueda y excluirán de la clasificación. Si tiene un conjunto grande de documentos, usar una profundización por facetas selectiva suele proporcionar un mayor rendimiento.
  
**Filtrar solo los campos por facetas Hola**

En por facetas exploración en profundidad, probablemente le interese tooonly incluir documentos que tienen valor de faceta de hello en un campo específico (con facetas), no en cualquier lugar en todos los campos de búsqueda. Agregar un filtro refuerza el campo de destino de hello dirigiendo Hola servicio toosearch sólo en campo con facetas de Hola para un valor coincidente.

**Recorte de los resultados de faceta con más filtros**

Resultados de la faceta son documentos que se encuentra en los resultados de búsqueda de Hola que coinciden con un término de la faceta. Hola siguiente ejemplo, en los resultados de búsqueda para *la informática en nube*, 254 elementos también tienen *especificación interno* como un tipo de contenido. Los elementos no son necesariamente excluyentes mutuamente. Si un elemento cumple los criterios de Hola de ambos filtros, se cuenta en cada uno de ellos. Esta duplicación es posible cuando facetas en `Collection(Edm.String)` campos, que son a menudo utilizan tooimplement documento etiquetado.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

En general, si encuentra que los resultados de faceta constantemente son demasiado grandes, se recomienda agregar más filtros toogive a los usuarios más opciones para restringir la búsqueda de Hola.

### <a name="tips-about-result-count"></a>Sugerencias sobre el recuento de resultados

**Limitar el número de elementos de navegación de la faceta de Hola Hola**

Para cada campo con facetas en el árbol de navegación de hello, hay un límite predeterminado de 10 valores. Este valor predeterminado relacione con estructuras de navegación porque mantiene valores de hello tamaño administrable tooa de lista. Puede invalidar Hola predeterminado asignando un valor toocount.

* `&facet=city,count:5`Especifica que solo Hola cinco primeras ciudades encuentra en la parte superior de hello clasificada los resultados se devuelven como resultado de la faceta. Considere una consulta de ejemplo con un término de búsqueda "aeropuerto" y 32 coincidencias. Si especifica la consulta de hello `&facet=city,count:5`solo cinco primeras ciudades Hola con hello se incluye la mayoría de los documentos en los resultados de búsqueda de hello en Hola resultados de la faceta.

Aviso Hola distinción entre los resultados de la faceta y resultados de la búsqueda. Resultados de la búsqueda son todos los documentos de Hola que coinciden con la consulta de Hola. Resultados de la faceta son Hola coincidencias para cada valor de faceta. En el ejemplo de Hola, resultados de búsqueda incluyen nombres de ciudades que no están en la lista de clasificaciones de faceta de hello (5 en nuestro ejemplo). Los resultados que se filtran mediante la navegación por facetas son visibles cuando se borran las facetas o se eligen otras facetas además de City. 

> [!NOTE]
> Analizar `count` cuando hay más de un tipo puede ser confuso. Hello tabla siguiente ofrece un breve resumen de cómo se utiliza el término de hello en la API de búsqueda de Azure, código de ejemplo y documentación. 

* `@colorFacet.count`<br/>
  En el código de presentación, debería ver un parámetro de recuento en faceta de hello, toodisplay usado Hola número de resultados de la faceta. En los resultados de faceta, número indica número de Hola de documentos que coinciden en términos de faceta de Hola o intervalo.
* `&facet=City,count:12`<br/>
  En una consulta de faceta, puede establecer el valor del recuento tooa.  valor predeterminado de Hello es 10, pero puede establecerlo superior o inferior. Establecer `count:12` obtiene Hola primeras 12 coincidencias en los resultados de la faceta por el número de documento.
* "`@odata.count`"<br/>
  En respuesta a la consulta hello, este valor indica el número de Hola de elementos coincidentes en los resultados de búsqueda de Hola. En promedio, es mayor que la suma de Hola de todos los resultados de faceta combinada debido toohello presencia de elementos que coinciden con el término de búsqueda de hello, pero no tener ninguna coincidencia del valor de faceta.

**Obtención de recuentos en los resultados de faceta**

Cuando se agrega una consulta por facetas de filtro tooa, conviene instrucción de faceta de hello tooretain (por ejemplo, `facet=Rating&$filter=Rating ge 4`). Técnicamente, faceta = clasificación no se necesita, pero manteniéndolo devuelve recuentos de Hola de los valores de facetas para las clasificaciones de 4 y versiones posteriores. Por ejemplo, si hace clic en "4" y Hola consulta incluye un filtro para mayor o igual demasiado "4", se devuelven recuentos para cada clasificación que es 4 y versiones posteriores.  

**Garantía de obtención de recuentos de faceta adecuados**

En determinadas circunstancias, es posible que los recuentos de faceta no coinciden con los conjuntos de resultados de hello (vea [la navegación por facetas en búsqueda de Azure (entrada de foro)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

Recuentos de faceta pueden ser incorrectos debido toohello arquitectura de partición. Cada índice de búsqueda tiene varias particiones, y cada partición notifica facetas de hello N principales por número de documento, que se combina en un único resultado. Si algunas particiones tienen muchos valores coincidentes, mientras que otros usuarios tengan menos, es posible que algunos valores de facetas faltan o bajo con recuento de resultados de Hola.

Aunque este comportamiento podría cambiar en cualquier momento, si se produce este comportamiento hoy en día, también puede trabajar a su alrededor artificialmente que infla recuento hello:<number> número de tooenforce grandes números de tooa completa de generación de informes de cada partición. Si Hola valor de recuento: es igual o mayor que toohello número de valores únicos en el campo de hello, se garantiza resultados precisos. Sin embargo, si el recuento de documentos es alto, esto afecta al rendimiento, por lo que debe usar esta opción con prudencia.

### <a name="user-interface-tips"></a>Sugerencias de interfaz de usuario
**Agregar etiquetas para cada campo en la navegación por facetas**

Las etiquetas se definen normalmente en hello HTML o un formulario (`index.cshtml` en la aplicación de ejemplo de Hola). No hay ninguna API en Azure Search para las etiquetas de navegación por facetas u otros tipos de metadatos.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Filtro basado en un intervalo
El uso de facetas en intervalos de valores es un requisito habitual de las aplicaciones de búsqueda. Se admiten intervalos para datos numéricos y valores de fecha y hora. Puede leer más acerca de cada enfoque en [Buscar documentos (API de Búsqueda de Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

Búsqueda de Azure simplifica la construcción de intervalos mediante dos enfoques de cálculo de intervalos. Para ambos enfoques, búsqueda de Azure crea Hola intervalos adecuados dados entradas de Hola que ha proporcionado. Por ejemplo, si especifica valores de intervalo de 10|20|30, creará automáticamente los intervalos 0-10, 10-20, 20-30. La aplicación tiene la opción de quitar los intervalos que estén vacíos. 

**Enfoque 1: Usar el parámetro de intervalo de hello**  
facetas de precio tooset en incrementos de 10 $, especificaría:`&facet=price,interval:10`

**Enfoque 2: Usar una lista de valores**  
Para datos numéricos, puede usar una lista de valores.  Considere la posibilidad de intervalo de faceta de Hola para un `listPrice` procesar el campo, como se indica a continuación:

  ![Lista de valores de ejemplo][5]

toospecify un intervalo de faceta como Hola uno Hola anterior captura de pantalla, utilice una lista de valores:

    facet=listPrice,values:10|25|100|500|1000|2500

Cada intervalo se compila utilizando 0 como punto de partida, un valor de lista de Hola como un punto de conexión y, a continuación, se recortan de intervalos discretos de hello anterior rangos toocreate. Azure Search hace esto como parte de la navegación por facetas. No tiene código toowrite para estructurar cada intervalo.

### <a name="build-a-filter-for-a-range"></a>Creación de un filtro para un intervalo
documentos de toofilter basadas en un intervalo que seleccione, puede usar hello `"ge"` y `"lt"` operadores en una expresión de dos partes que define los puntos de conexión de Hola de intervalo de Hola de filtro. Por ejemplo, si elige Hola intervalo 10-25 para un `listPrice` campo, filtro de hello sería `$filter=listPrice ge 10 and listPrice lt 25`. En el código de ejemplo de Hola, usa la expresión de filtro de hello **priceFrom** y **priceTo** puntos de conexión de parámetros tooset Hola. 

  ![Consulta para un intervalo de valores][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Filtro basado en la distancia
Su toosee comunes filtros que le ayudan a elegir un almacén, restaurante o un destino basándose en su ubicación actual de tooyour de proximidad. Aunque este tipo de filtro puede parecer una navegación por facetas, en realidad es solo un filtro. Lo mencionamos aquí para aquellos que buscan específicamente consejos de implementación para ese problema de diseño concreto.

Hay dos funciones geoespaciales en Azure Search, **geo.distance** y **geo.intersects**.

* Hola **geo.distance** función devuelve la distancia de hello en kilómetros entre dos puntos. Un punto es un campo y otra es una constante que se pasa como parte del filtro de Hola. 
* Hola **geo.intersects** función devuelve true si un punto determinado se encuentra dentro de un polígono determinado. punto de Hello es un campo y Hola polígono se especifica como una lista de constante de coordenadas que se pasa como parte del filtro de Hola.

Puede encontrar ejemplos de filtros en [Sintaxis de expresiones de OData (Búsqueda de Azure)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Pruebe Hola demostración
Hola demostración de Portal de trabajo de búsqueda de Azure contiene ejemplos de hello hace referencia en este artículo.

-   Ver y probar demostración en línea de hello trabajar en [demostración de Portal de trabajo de búsqueda de Azure](http://azjobsdemo.azurewebsites.net/).

-   Descargar código de hello de hello [repositorio de ejemplos de Azure en GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Cuando se trabaja con los resultados de búsqueda, vea Hola URL para los cambios en la construcción de consultas. Esta aplicación produce tooappend facetas toohello URI mientras selecciona cada uno de ellos.

1. funcionalidad de asignación de hello toouse de aplicación de demostración de hello, obtener una clave de mapas de Bing de hello [centro de desarrollo de mapas de Bing](https://www.bingmapsportal.com/). Péguela sobre clave existente de Hola Hola `index.cshtml` página. Hola `BingApiKey` en hello `Web.config` no se utiliza el archivo. 

2. Ejecute la aplicación hello. Paseo opcional de Hola o descartar el cuadro de diálogo de Hola.
   
3. Escriba un término de búsqueda, como "analista" y haga clic en el icono de búsqueda de Hola. consulta de Hola se ejecuta rápidamente.
   
   También se devuelve una estructura de navegación por facetas con resultados de la búsqueda de Hola. En la página de resultados de búsqueda de hello, estructura de navegación por facetas de hello incluye recuentos de cada resultado de la faceta. No hay facetas seleccionadas, por lo que se devuelven todos los resultados de búsqueda que coinciden.
   
   ![Resultados de la búsqueda antes de seleccionar las facetas][11]

4. Haga clic en un Business Title (cargo empresarial), Location (ubicación) o Minimum Salary (salario mínimo). Facetas eran nulos en la búsqueda inicial de hello, pero tal y como asumen los valores, los resultados de la búsqueda de Hola se recortan de elementos que ya no coinciden con.
   
   ![Resultados de la búsqueda después de seleccionar las facetas][12]

5. consulta por facetas de hello tooclear por lo que puede probar comportamientos de consulta diferente, haga clic en hello `[X]` después de hello seleccionado facetas de facetas tooclear Hola.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>Más información
Vea el vídeo de [profundización en Azure Search](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410). En 45:25, hay una demostración acerca de cómo tooimplement facetas.

Para más información sobre los principios de diseño para la navegación por facetas, se recomienda Hola siguientes vínculos:

* [Diseñar para la búsqueda por facetas](http://www.uie.com/articles/faceted_search/)
* [Patrones de diseño: Navegación por facetas](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

