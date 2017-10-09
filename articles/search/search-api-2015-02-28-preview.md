---
title: "aaaAzure búsqueda servicio REST API versión 2015-02-28-vista previa | Documentos de Microsoft"
description: "La API de REST del Servicio Búsqueda de Azure versión 2015-02-28-Preview incluye funciones experimentales como analizadores de lenguaje Natural y búsquedas moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>API de REST del Servicio Búsqueda de Azure versión 2015-02-28-Preview
Este artículo es la documentación de referencia de Hola para `api-version=2015-02-28-Preview`. Esta vista previa extiende versión disponible con carácter general actual hello, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), proporcionando Hola siguiendo las características experimentales:

* `moreLikeThis`parámetro Hola consulta [buscar documentos](#SearchDocs) API. Busca otros documentos que son relevantes tooanother documento específico.

Algunas partes adicionales de hello `2015-02-28-Preview` API de REST se documentan por separado. Entre ellos se incluyen los siguientes:

* [Perfiles de puntuación](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indexadores](search-api-indexers-2015-02-28-preview.md)

El servicio de Búsqueda de Azure está disponible en varias versiones. Consulte demasiado[versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información.

## <a name="apis-in-this-document"></a>API incluidas en este documento
La API del servicio Búsqueda de Azure admite dos sintaxis de URL para operaciones de API: simple y OData (consulte [Compatibilidad con OData (API de Búsqueda de Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obtener más información). Hello lista siguiente muestra una sintaxis sencilla Hola.

[Crear índice](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Actualizar índice](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Obtener índice](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Enumerar índices](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Obtención de estadísticas de índice](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Analizador de prueba](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Eliminar un índice](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Agregar, eliminar y actualizar datos en un índice](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Buscar en documentos](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Buscar documento](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Documentos de recuento](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Sugerencias](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Operaciones de índice
Puede crear y administrar índices en el servicio de Búsqueda de Azure a través de solicitudes HTTP sencillas (POST, GET, PUT, DELETE) en un recurso de índice determinado. toocreate un índice, REGISTRE primero un documento JSON que describe el esquema de índice Hola. esquema de Hello define los campos de Hola de índice de hello, sus tipos de datos y cómo se puede usar (por ejemplo, en las búsquedas de texto completo, filtros, ordenación o facetas). También define los perfiles de puntuación, proveedores de sugerencias y otros comportamientos de hello tooconfigure de atributos de índice de Hola.

Hello en el ejemplo siguiente se proporciona una ilustración de un esquema utilizado para buscar información sobre hoteles con campo de descripción de hello definido en dos idiomas. Observe cómo los atributos controlan cómo se utiliza el campo de Hola. Por ejemplo Hola `hotelId` se utiliza como clave de documento de hello (`"key": true`) y se excluye de búsquedas de texto completo (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Después de crea el índice de hello, podrá cargar documentos que rellenan índice Hola. Consulte [Agregar o actualizar documentos](#AddOrUpdateDocuments) para este siguiente paso.

Para tooindexing de vídeo de introducción en búsqueda de Azure, vea hello [episodio de Cloud Cover de Channel 9 sobre búsqueda de Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Crear índice
Un índice es el medio principal de Hola de organizar y buscar documentos en búsqueda de Azure, toohow similar una tabla organiza los registros en una base de datos. Cada índice tiene una colección de documentos que conformes toohello esquema de índice (nombres de campo, tipos de datos y propiedades), pero los índices también especifican construcciones adicionales (proveedores de sugerencias, perfiles de puntuación y opciones de CORS) que definen otros comportamientos de búsqueda.

Puede crear un índice nuevo dentro de un servicio de Búsqueda de Azure mediante una solicitud HTTP POST o PUT. cuerpo de saludo de solicitud de hello es un esquema JSON que especifica la información de índice y la configuración de Hola.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Como alternativa, puede usar PUT y especificar el nombre del índice de hello en hello URI. Si el índice de hello no existe, se creará.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Crear un índice determina la estructura de Hola de hello documentos almacenados y utilizados en operaciones de búsqueda. Rellenar índice hello es una operación independiente. En este paso, puede usar un [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponible para orígenes de datos admitidos) o una operación [Agregar, actualizar o eliminar documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx). índice Hola invertido se genera cuando se publican los documentos de Hola.

**Tenga en cuenta**: Hola número máximo de índices permitidos varía según el nivel de precios. servicio gratuito de Hello permite que los índices de too3. El servicio estándar permite 50 índices por servicio de búsqueda. Consulte [Límites y restricciones](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obtener detalles.

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Hola **Create Index** solicitud puede crearse mediante un método POST o PUT. Al usar POST, debe proporcionar un nombre de índice en el cuerpo de la solicitud junto con la definición de esquema de índice de Hola Hola. Con PUT, el nombre del índice de hello es parte de la dirección URL de Hola. Si el índice de hello no existe, se crea. Si ya existe, está actualizada toohello nueva definición.

nombre del índice Hola debe estar en minúsculas, empezar por una letra o un número, no tener barras o puntos y tener menos de 128 caracteres. Después de iniciar el nombre del índice de hello con una letra o un número, rest Hola de nombre de hello puede incluir cualquier letra, número y guiones, como Hola guiones no sean consecutivos.

Hola `api-version` es necesario. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener una lista de las versiones disponibles.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `Content-Type`: obligatorio. Establezca esta propiedad demasiado`application/json`
* `api-key`: obligatorio. Hola `api-key` se usa para
* autenticar el servicio de búsqueda de hello solicitud tooyour. Es un valor de cadena, el servicio de tooyour único. Hola **Create Index** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Se puede obtener el nombre de servicio hello y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

<a name="RequestData"></a>
**Sintaxis del cuerpo de la solicitud**

Hola el cuerpo de solicitud de hello contiene una definición de esquema, que incluye Hola lista de campos de datos dentro de los documentos que se introducirán en este índice, tipos de datos, atributos, así como una lista opcional de los perfiles de puntuación es utilizado tooscore coincidencia de documentos en tiempo de consulta.

Tenga en cuenta que para una solicitud POST, debe especificar el nombre del índice de Hola Hola del cuerpo de solicitud.

Solo puede haber un campo de clave de índice de Hola. Tiene un campo de cadena toobe. Este campo representa el identificador único de Hola para cada documento almacenado en el índice de Hola.

partes principales de Hola de un índice Hola siguientes:

* `name`
* `fields` que se introducirán en este índice, incluido el nombre, tipo de datos y propiedades que definen las acciones permitidas en ese campo.
* `suggesters` se usa para autocompletar o anticipar la escritura de las consultas.
* `scoringProfiles` se usa para la clasificación de la puntuación de la búsqueda personalizada. Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utiliza toodefine cómo las documentos y consultas se dividen en tokens indizable/permite realizar búsquedas. Consulte [Análisis en Búsqueda de Azure](https://aka.ms//azsanalysis) para más detalles.
* `defaultScoringProfile`Usar valor predeterminado de hello toooverwrite comportamientos de puntuación.
* `corsOptions`consultas entre orígenes de tooallow sobre el índice.

sintaxis de Hola para estructurar la carga de la solicitud de hello es como sigue. En este tema se proporciona una solicitud de ejemplo.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Atributos de índice**

Hello atributos siguientes pueden establecerse al crear un índice. Para obtener más información sobre la puntuación y los perfiles de puntuación, consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Conjuntos Hola nombre del campo de Hola.

`type`-Conjuntos Hola tipo de datos de campo de Hola.

`searchable`-Marca Hola campo como texto completo capacitado para búsquedas. Esto significa que se someterá a análisis como la separación de palabras durante la indexación. Si establece un `searchable` valor del campo tooa como "sunny day", internamente será dividir en tokens individuales Hola "sunny" y "día". Esto permite realizar búsquedas de texto completo de estos términos. Los campos de tipo `Edm.String` o `Collection(Edm.String)` son `searchable` de manera predeterminada. Los campos de otros tipos no pueden ser `searchable`.

* **Tenga en cuenta**: `searchable` campos consumen espacio adicional en el índice, ya que la búsqueda de Azure almacenará una versión con tokens adicional del valor de campo de Hola para búsquedas de texto completo. Si desea toosave espacio en el índice y no es necesario un toobe de campo que se incluyen en las búsquedas, establezca `searchable` demasiado`false`.

`filterable`: Permite hello toobe de campo al que hace referencia en `$filter` las consultas. `filterable` difiere de `searchable` en el modo en que se gestionan las cadenas. Los campos de tipo `Edm.String` o `Collection(Edm.String)` que son `filterable` no sufren separación de palabras, por lo que las comparaciones son solo para las coincidencias exactas. Por ejemplo, si establece este tipo de campo `f` demasiado "sunny day", `$filter=f eq 'sunny'` encontrará ninguna coincidencia, pero `$filter=f eq 'sunny day'` le. Todos los campos son `filterable` de forma predeterminada.

`sortable`-Predeterminada Hola sistema ordena los resultados por puntuación, pero en muchas ocasiones los usuarios desearán toosort por campos de documentos de Hola. Los campos de tipo `Collection(Edm.String)` no pueden ser `sortable`. El resto de campos son `sortable` de forma predeterminada.

`facetable`: suele utilizarse en una presentación de resultados de búsqueda que incluya el número de resultados por categoría (por ejemplo, busque cámaras digitales y consulte los resultados divididos por marca, por megapíxeles, por precio, etc.). Esta opción no puede utilizarse con campos de tipo `Edm.GeographyPoint`. El resto de campos son `facetable` de forma predeterminada.

* **Nota**: los campos de tipo `Edm.String` que son `filterable`, `sortable` o `facetable` solo pueden ocupar una longitud de 32 KB como máximo. Esto es porque esos campos se tratan como un término de búsqueda sencillo, y la longitud máxima de Hola de un término de búsqueda de Azure es 32KB. Si necesita toostore texto más que la especificada en un campo de cadena único, deberá tooexplicitly establecer `filterable`, `sortable`, y `facetable` demasiado`false` en la definición del índice.
* **Tenga en cuenta**: si un campo no tiene ninguno de hello anterior atributos se establecen demasiado`true` (`searchable`, `filterable`, `sortable`, o`facetable`) campo Hola se excluye eficazmente del índice de hello invertido. Esta opción es útil para los campos que no se utilizan en las consultas, pero que son necesarios en los resultados de la búsqueda. Exclusión de esos campos del índice de hello mejora el rendimiento.

`key`-Marcas Hola campo como que contiene identificadores únicos para los documentos en el índice de Hola. Se debe elegir exactamente un campo como hello `key` campo y debe ser de tipo `Edm.String`. Campos clave pueden ser utilizado toolook documentos directamente a través de hello [API de búsqueda](#LookupAPI).

`retrievable`-Establece si el campo de Hola se puede devolver resultados de la búsqueda.  Esto es útil cuando se desea toouse un campo (por ejemplo, margen) como un filtro, ordenación o puntuación mecanismo pero no desea que el usuario final toohello visible de hello campo toobe. Este atributo debe ser `true` for `key` .

`analyzer`-Conjuntos Hola nombre de hello analizador toouse campo hello en tiempo de búsqueda y el momento de la indización. Encontrará Hola conjunto de valores permitido [analizadores](https://msdn.microsoft.com/library/mt605304.aspx). Esta opción puede utilizarse solo con campos `searchable` y no se puede establecer junto con `searchAnalyzer` o `indexAnalyzer`.  Una vez que se elige el analizador de hello, no se puede cambiar para el campo de Hola.

`searchAnalyzer`-Conjuntos Hola nombre del analizador de Hola que se usa en tiempo de búsqueda para el campo de Hola. Encontrará Hola conjunto de valores permitido [analizadores](https://msdn.microsoft.com/library/mt605304.aspx). Esta opción solo puede utilizarse con campos `searchable` . Debe establecerse junto con `indexAnalyzer` y no se puede establecer junto con hello `analyzer` opción. Este analizador se puede actualizar en un campo existente.

`indexAnalyzer`-Conjuntos Hola nombre del analizador de hello usada en tiempo de indización para el campo de Hola. Encontrará Hola conjunto de valores permitido [analizadores](https://msdn.microsoft.com/library/mt605304.aspx). Esta opción solo puede utilizarse con campos `searchable` . Debe establecerse junto con `searchAnalyzer` y no se puede establecer junto con hello `analyzer` opción. Una vez que se elige el analizador de hello, no se puede cambiar para el campo de Hola.

`suggesters`-Conjuntos Hola a modo de búsqueda y campos que son origen de Hola de contenido de Hola para obtener sugerencias. Consulte [Proveedores de sugerencias](#Suggesters) para obtener más información.

`scoringProfiles` : define comportamientos de puntuación personalizados que permiten influir en los elementos que aparecen más arriba en los resultados de la búsqueda. Los perfiles de puntuación se componen de ponderaciones de campos y de funciones. Vea [agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información sobre atributos de hello usados en un perfil de puntuación.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Compatibilidad con idioma**

Los campos localizables se someten a análisis que con frecuencia implican la separación de palabras, la normalización de texto y el filtrado de términos. De forma predeterminada, los campos de búsqueda en búsqueda de Azure se analizan con hello [analizador estándar Lucene de Apache](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que divide el texto en los elementos que siguen la["Segmentación de texto Unicode"](http://unicode.org/reports/tr29/) reglas. Además, analizador estándar Hola convierte formato en todos los caracteres tootheir minúsculas. Los documentos indizados y términos de búsqueda van a través del análisis de Hola durante la indización y procesamiento de consultas.

Búsqueda de Azure admite una variedad de lenguajes. Cada uno de esos idiomas requiere un analizador de texto no estándar que representa las características de un idioma determinado. Búsqueda de Azure ofrece dos tipos de analizadores:

* 35 analizadores respaldados por Lucene.
* 50 analizadores respaldados por la tecnología de procesamiento de lenguaje natural de Microsoft usada en Office y Bing.

Algunos desarrolladores de software podría ser preferible Hola solución mucho más familiar, simple, código abierto de Lucene. Analizadores de Lucene son más rápidos, pero analizadores de Microsoft hello tienen capacidades, como la lematización avanzadas, decompounding (en idiomas como el alemán, danés, neerlandés, sueco, noruego, estonio, finalizar, húngaro, eslovaco) y reconocimiento de entidades (las direcciones URL de word mensajes de correo electrónico, fechas, números). Si es posible, debe ejecutar las comparaciones de ambos toodecide Hola Microsoft y Lucene analizadores cuál es mejor.

***Cómo se comparan***

Analizador de Lucene de Hola para inglés amplía el analizador estándar Hola. Elimina los posesivos (los ’s finales) de las palabras, aplica la lematización conforme al [Algoritmo de lematización Porter](http://tartarus.org/~martin/PorterStemmer/) y elimina las [palabras no significativas](http://en.wikipedia.org/wiki/Stop_words) del inglés.

En comparación, analizador de Microsoft hello realiza lematización en lugar de lematización. Significa que puede controlar mucho mejor formas de palabras derivadas e irregulares, lo que da como resultado unos resultados de búsqueda más pertinentes (consulte el módulo 7 de [presentación MVA de Búsqueda de Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obtener más detalles).

La indización con analizadores de Microsoft por término medio es dos veces toothree más lentos que sus equivalentes de Lucene, según el lenguaje de Hola. El rendimiento de la búsqueda no debería verse afectado significativamente en las consultas de tamaño medio.

***Configuración***

Para cada campo en la definición del índice hello, puede establecer hello `analyzer` nombre del analizador de tooan propiedad que especifica qué idioma y el proveedor. Hola mismo analizador se aplicarán cuando la indización y búsqueda para ese campo.
Por ejemplo, puede tener campos separados para descripciones de hoteles inglés, francés y español que existen en paralelo en hello mismo índice. Hola de uso ['searchFields' parámetro de consulta](#SearchQueryParameters) toospecify qué toosearch de campo específico del idioma en las consultas. Puede revisar los ejemplos de consultas que incluyen hello `analyzer` propiedad en [buscar documentos](#SearchDocs). 

***Lista de analizadores***

A continuación se muestra la lista de Hola de idiomas admitidos junto con los nombres de analizador de Lucene y Microsoft.

<table style="font-size:12">
    <tr>
        <th>language</th>
        <th>Nombre del analizador de Microsoft</th>
        <th>Nombre del analizador de Lucene</th>
    </tr>
    <tr>
        <td>Árabe</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Armenio</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>Bangla</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Vasco</td>
        <td></td>
        <td>eu.Lucene</td>
    </tr>
      <tr>
         <td>Búlgaro</td>
        <td>bg.microsoft</td>
        <td>bg.lucene</td>
      </tr>
      <tr>
        <td>Catalán</td>
        <td>ca.microsoft</td>
        <td>ca.lucene</td>          
      </tr>
    <tr>
        <td>Chino simplificado</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Chino tradicional</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Croata</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Checo</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>Danés</td>
        <td>da.microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Neerlandés</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>English</td>        
        <td>en.microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estonio</td>
        <td>et.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Finés</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>Francés</td>
        <td>fr.microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>Gallego</td>
        <td></td>
        <td>gl.lucene</td>        
      </tr>
    <tr>
        <td>Alemán</td>
        <td>de.microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Griego</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Gujarati</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hebreo</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hindi</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>Húngaro</td>        
        <td>hu.microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>Islandés</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonesio (Bahasa)</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>Irlandés</td>
        <td></td>
          <td>ga.lucene</td>
    </tr>
    <tr>
        <td>Italiano</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>Japonés</td>
        <td>ja.microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Coreano</td>
        <td>ko.Microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>Letón</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>Lituano</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayalam</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayo (latino)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Noruego</td>
        <td>nb.microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>Persa</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>Polaco</td>
        <td>pl.microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>Portugués (Brasil)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>Portugués (Portugal)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>Punjabi</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Rumano</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Ruso</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>Serbio (cirílico)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Serbio (latino)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Eslovaco</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Esloveno</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Español</td>
        <td>es.Microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>Sueco</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>Tamil</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Telugu</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Tailandés</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>Turco</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>Ucraniano</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urdu</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnamita</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Además, Búsqueda de Azure proporciona las configuraciones del analizador de lenguaje válido</td>
    <tr>
        <td>Plegamiento de ASCII estándar</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Segmentación de texto Unicode (Tokenizer estándar)</li>
            <li>Filtro de conversión de ASCII - convierte los caracteres Unicode que no pertenecen toohello conjunto de los primeros 127 caracteres ASCII en sus valores ASCII equivalentes. Esto es útil para quitar los signos diacríticos.</li>
        </ul>
        </td>
    </tr>
</table>

Todos los analizadores con nombres anotados con <i>lucene</i> disponen de tecnología de [analizadores de idioma de Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Puede encontrar más información sobre el filtro de conversión de ASCII de hello [aquí](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Proveedores de sugerencias**

Un `suggester` define qué campos en un índice son utilizado toosupport Autocompletar en las búsquedas. Normalmente, las cadenas de búsqueda parcial se envían toohello [API sugerencias](#Suggestions) mientras el usuario de hello está escribiendo una consulta de búsqueda y Hola API devuelve un conjunto de frases sugeridas. Un proveedor de sugerencias que defina en el índice de hello determina qué campos son los términos de búsqueda anticipada de hello toobuild usado. Consulte [Proveedores de sugerencias](#Suggesters) para obtener más detalles sobre la configuración.

**Perfiles de puntuación**

Un `scoringProfile` define los comportamientos de puntuación personalizados que pueden influir en los elementos que aparecen más arriba en resultados de búsqueda de Hola. Los perfiles de puntuación se componen de ponderaciones de campos y de funciones. toouse usarlas, se especifica un perfil por nombre en la cadena de consulta de Hola.

Un perfil de puntuación predeterminado funciona en segundo Hola plano toocompute una puntuación de búsqueda para todos los elementos de un conjunto de resultados. Puede usar Hola interno, sin nombre perfil de puntuación. Por otra parte, defina `defaultScoringProfile` toouse un perfil personalizado como Hola de forma predeterminada, se invoca cuando un perfil personalizado no se especifica en la cadena de consulta de Hola.

Vea [puntuación agregar perfiles de índice de búsqueda tooa (API de REST de servicio de búsqueda de Azure)](search-api-scoring-profiles-2015-02-28-preview.md) para obtener más información.

**Opciones de CORS**

Javascript del lado cliente no puede llamar a las API de forma predeterminada, ya que el Explorador de hello impedirá todas las solicitudes entre orígenes. Habilitar CORS (uso compartido recursos entre orígenes) por establecer hello `corsOptions` índice tooyour de atributo tooallow consultas entre orígenes. Tenga en cuenta que solamente las API de consulta admiten CORS por motivos de seguridad. Hola siguientes opciones se pueden establecer para CORS:

* `allowedOrigins`(obligatorio): se trata de una lista de orígenes que se le concederá el índice de tooyour de acceso. Esto significa que cualquier código de Javascript que se sirva desde esos orígenes permite tooquery su índice (suponiendo proporciona la clave de API correcta de hello). Cada origen suele del formulario de hello `protocol://fully-qualified-domain-name:port` aunque a menudo se omite el puerto de Hola. Consulte [este artículo](http://go.microsoft.com/fwlink/?LinkId=330822) para obtener más detalles.
  * Si desea que los orígenes de tooall de acceso tooallow, incluya `*` como un único elemento de hello `allowedOrigins` matriz. Tenga en cuenta que **esta no es una práctica recomendada para los servicios de búsqueda de producción.** Sin embargo, puede ser útil para el desarrollo o con fines de depuración.
* `maxAgeInSeconds`(opcional): los exploradores utilizan este las respuestas preparatorias de CORS toocache de valor toodetermine Hola duración (en segundos). Esto debe ser un entero no negativo. Hola mayor que es este valor, será un mejor rendimiento de hello, pero hello más tiempo que tardará CORS directiva cambios tootake efecto. Si no se establece, se usará una duración predeterminada de 5 minutos.

<a name="CreateUpdateIndexExample"></a>
**Ejemplo de cuerpo de solicitud**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Respuesta**

Para obtener una solicitud correcta: "201 Creado".

De forma predeterminada cuerpo de respuesta de hello contendrá hello JSON para la definición de índice de Hola que se creó. Si hello `Prefer` encabezado de solicitud se establece demasiado`return=minimal`, cuerpo de respuesta de hello estará vacío y código de estado de hello correcto será "204 Sin contenido" en lugar de "201 Created". Esto es cierto independientemente de si PUT o POST estaba índice de hello toocreate usado.

**Comentarios**

Actualmente, hay compatibilidad limitada para las actualizaciones del esquema de índice. Actualmente no se admiten las actualizaciones del esquema que requieran volver a indexar, como el cambio de tipos de campo. Aunque no se puede cambiar los campos existentes o eliminado los campos nuevos se pueden agregar índice existente tooan en cualquier momento. Cuando se agrega un nuevo campo, todos los documentos existentes en el índice de hello automáticamente tendrá un valor null para ese campo. No hay espacio de almacenamiento adicional se consumirán hasta que se agreguen nuevos documentos toohello índice.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Proveedores de sugerencias
característica de sugerencias de Hello en búsqueda de Azure es una capacidad de consulta anticipada o Autocompletar, que proporciona una lista de posibles términos de búsqueda en respuesta toopartial las entradas de cadena especificadas en un cuadro de búsqueda. Probablemente haya observado sugerencias de consulta al utilizar los motores de búsqueda web comerciales: si se escribe ".NET" en Bing, se genera una lista de términos para ".NET 4.5", ".NET Framework 3.5", y así sucesivamente. Cuando se usa el servicio de búsqueda de hello API de REST, implementación de sugerencias en una aplicación de búsqueda de Azure personalizada requiere siguiente hello:

* Habilite sugerencias agregando una **proveedor de sugerencias** construcción en el índice, se ha dado nombre hello, modo de búsqueda y una lista de campos para que anticipada se invoca. Por ejemplo, si especifica "cityName" como un campo de origen, escriba una cadena de búsqueda parcial del "Mar" dará como resultado "Seattle", "Seaside" y "Seatac" (las tres son nombres de ciudades reales) presenten como usuario de toohello de sugerencias de consulta.
* Invocar sugerencias que realiza la llamada hello [API sugerencias](#Suggestions) en el código de aplicación. Normalmente las cadenas de búsqueda parcial se envían toohello servicio mientras Hola usuario escribe una consulta de búsqueda, y esta API devuelve un conjunto de frases sugeridas.

Este artículo se explica cómo tooconfigure una **proveedor de sugerencias**. También debe revisar hello [API sugerencias](#Suggestions) para obtener más información sobre cómo se utiliza un proveedor de sugerencias.

**Uso**

`Suggesters`se crean en el índice de Hola y funcionan mejor cuando se usa toosuggest específicos se documentan en lugar de términos o frases sueltos. campos de Hello más recomendados son títulos, nombres y demás frases relativamente cortas que puedan identificar un elemento. Los campos repetitivos son menos efectivos, por ejemplo, las categorías y etiquetas, o campos muy largos como campos de descripciones o comentarios.

Como parte de la definición del índice hello, puede agregar un único proveedor de sugerencias toohello `suggesters` colección. Propiedades que definen un proveedor de sugerencias Hola siguientes:

* `name`: nombre de hello del proveedor de sugerencias de Hola. Usar nombre de hello del proveedor de sugerencias de hello al llamar a hello `suggest` API.
* `searchMode`: Hola toosearch estrategia que se usa para frases candidatas. Hola único modo que admite actualmente es `analyzingInfixMatching`, que realiza una coincidencia flexible de frases al principio de Hola o en medio de Hola de oraciones.
* `sourceFields`: Una lista de uno o más campos que son origen de hello del contenido de Hola para obtener sugerencias. Solo los campos de tipo `Edm.String` y `Collection(Edm.String)` pueden ser orígenes para obtener sugerencias. Solo se pueden usar los campos que no tienen un analizador de lenguaje personalizado establecido.

**Ejemplo de proveedor de sugerencias**

Un proveedor de sugerencias es parte del índice de Hola. Puede haber solo un proveedor de sugerencias en hello `suggesters` colección de campos de la colección en la versión actual de hello, junto con hello y `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Si ha usado la versión de vista previa pública de Hola de búsqueda de Azure, `suggesters` reemplaza una propiedad booleana más antigua (`"suggestions": false`) que solo admitía sugerencias de prefijo para cadenas cortas (3-25 caracteres). Su reemplazo, `suggesters`, admite coincidencias de infijo que encuentra términos coincidentes al principio de Hola o en medio de Hola de contenido de este campo, con una mejor tolerancia a errores en las cadenas de búsqueda. A partir de la versión de disponibilidad general de hello, ahora es única implementación de sugerencias de hello API de Hola. Hola anterior `suggestions` propiedad que se introdujo en `api-version=2014-07-31-Preview` continúa toowork en esa versión, pero no está operativa en hello `2015-02-28` o versiones posteriores de búsqueda de Azure.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Actualizar índice
Puede actualizar un índice existente en Búsqueda de Azure mediante una solicitud HTTP PUT. Las actualizaciones pueden incluir agregar nuevos campos toohello esquema existente, modificar las opciones de CORS y modificar perfiles de puntuación. Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información. Especificar nombre de Hola de hello índice tooupdate en URI de solicitud de hello:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Importante:** compatibilidad con las actualizaciones de esquema de índice es toooperations limitada que no requieren volver a generar índice de búsqueda de Hola. Actualmente no se admiten las actualizaciones del esquema que requieran volver a indexar, como el cambio de tipos de campo. Pueden agregarse nuevos campos en cualquier momento, aunque no se pueden modificar ni eliminar los campos existentes. Hello Esto mismo se aplica demasiado`suggesters`. Pueden agregarse nuevos campos se agregan tooa proveedor de sugerencias en campos de Hola Hola hora, pero no se puede quitar campos `suggesters` y no se puede agregar campos existentes demasiado`suggesters`.

Al agregar un nuevo índice tooan de campo, todos los documentos existentes en el índice de hello automáticamente tendrá un valor null para ese campo. No hay espacio de almacenamiento adicional se consumirán hasta que se agreguen nuevos documentos toohello índice.

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Hola **Actualizar índice** solicitud se construye utilizando PUT de HTTP. Con PUT, el nombre del índice de hello es parte de la dirección URL de Hola. Si el índice de hello no existe, se crea. Si ya existe un índice de hello, es toohello actualizada nueva definición.

nombre del índice Hola debe estar en minúsculas, empezar por una letra o un número, no tener barras o puntos y tener menos de 128 caracteres. Después de iniciar el nombre del índice de hello con una letra o un número, rest Hola de nombre de hello puede incluir cualquier letra, número y guiones, como Hola guiones no sean consecutivos.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `Content-Type`: obligatorio. Establezca esta propiedad demasiado`application/json`
* `api-key`: obligatorio. Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **Actualizar índice** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Sintaxis del cuerpo de la solicitud**

Al actualizar un índice existente, el cuerpo de hello debe incluir la definición de esquema original de hello, además de nuevos campos de Hola que va a agregar, así como Hola modifica perfiles de puntuación, proveedores de sugerencias y las opciones de CORS, si existe. Si no va a modificar perfiles de puntuación de Hola y opciones de CORS, debe incluir los originales Hola de cuándo se creó el índice de Hola. Por lo general Hola mejor patrón toouse actualizaciones es definición del índice de hello tooretrieve con una operación GET, modificarlo, actualizarlo con PUT.

sintaxis de esquema de Hello utilizan toocreate que un índice se reproduce aquí por comodidad. Consulte [Crear índice](#CreateIndex) para obtener más detalles.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Respuesta**

Para obtener una solicitud correcta: "204 Sin contenido".

De forma predeterminada el cuerpo de la respuesta de hello estará vacío. Sin embargo, si hello `Prefer` encabezado de solicitud se establece demasiado`return=representation`, cuerpo de respuesta de hello contendrá hello JSON para la definición del índice Hola que se ha actualizado. En este caso, código de estado de hello correcto será "200 Aceptar".

**Actualización de definiciones de índices con analizadores personalizados**

Una vez definido un analizador, un tokenizador o un filtro de caracteres, no se puede modificar. Nuevos pueden agregarse índice existente tooan solo si hello `allowIndexDowntime` tootrue se establece una marca en la solicitud de actualización de índice de hello: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Tenga en cuenta que esta operación, se colocará el índice sin conexión al menos unos segundos, haciendo que la indización y consulta solicita toofail. Disponibilidad de rendimiento y la escritura del índice de hello puede ser afectado durante varios minutos después de haber actualizado el índice de Hola o más índices muy grandes.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Índices de la lista
Hola **índices de la lista** operación devuelve una lista de índices de hello actualmente en el servicio de búsqueda de Azure.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Hola **índices de la lista** solicitud puede crearse mediante el método GET de Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: obligatorio. Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **índices de la lista** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Ninguno.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

A continuación se proporciona un cuerpo de respuesta de ejemplo:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Tenga en cuenta que puede filtrar Hola respuesta hacia abajo de propiedades de hello toojust que le interesa. Por ejemplo, si desea que solo una lista de nombres de índice, use Hola OData `$select` opción de consulta:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

En este caso, respuesta Hola Hola ejemplo anterior podría aparecer como sigue:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Se trata de un ancho de banda de toosave técnica útil si tiene una gran cantidad de índices en el servicio de búsqueda.

<a name="GetIndex"></a>

## <a name="get-index"></a>Obtener índice
Hola **obtener índice** operación obtiene la definición del índice Hola de búsqueda de Azure.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Solicitud**

HTTPS es necesario para las solicitudes de servicio. Hola **obtener índice** solicitud puede crearse mediante el método GET de Hola.

Hola [nombre del índice] Hola URI de la solicitud especifica qué tooreturn de índice de la colección de índices de Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **obtener índice** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Ninguno.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

Vea el ejemplo de Hola JSON en [creación y actualización de un índice](#CreateUpdateIndexExample) para obtener un ejemplo de carga de respuesta de Hola.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Eliminar índice
Hola **Eliminar índice** operación quita un índice y los documentos asociados desde el servicio de búsqueda de Azure. Puede obtener el nombre del índice de Hola desde el panel de servicio de hello en hello portal de Azure o desde Hola API. Consulte [Índices de la lista](#ListIndexes) para obtener más información.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Solicitud**

HTTPS es necesario para las solicitudes de servicio. Hola **Eliminar índice** solicitud puede crearse mediante el método de eliminación de Hola.

Hola [nombre del índice] Hola URI de la solicitud especifica qué toodelete de índice de la colección de índices de Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: obligatorio. Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena único tooyour dirección URL del servicio. Hola **Eliminar índice** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Ninguno.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 204 Sin contenido.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Obtención de estadísticas de índice
Hola **obtener estadísticas de índice** operación devuelve de búsqueda de Azure, un número de documento para el índice actual de hello, además de uso de almacenamiento.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Se recopilan estadísticas del tamaño de almacenamiento y el número de documento cada pocos minutos; es decir, no se hace en tiempo real. Por lo tanto, las estadísticas de hello devueltas por esta API pueden no reflejar cambios causado por operaciones de indización recientes.
> 
> 

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Hola **obtener estadísticas de índice** solicitud puede crearse mediante el método GET de Hola.

Hola [nombre del índice] en el URI de solicitud de hello indica estadísticas de índice tooreturn Hola de servicio para el índice especificado de Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **obtener estadísticas de índice** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Ninguno.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

cuerpo de respuesta de Hello es Hola siguiendo el formato:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Analizador de prueba
Hola **API analizar** muestra cómo un analizador divide el texto en tokens.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Hola **API analizar** solicitud puede crearse mediante el método POST de Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **API analizar** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).

También necesitará el nombre del índice de Hola y Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

o

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Hola `analyzer_name`, `tokenizer_name`, `token_filter_name` y `char_filter_name` necesita toobe nombres válidos de analizadores predefinidos o personalizados, Tokenizer, token filtros y filtros de char para índice de Hola. toolearn más información sobre el proceso de Hola de análisis léxico vea [análisis en búsqueda de Azure](https://aka.ms/azsanalysis).

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

cuerpo de respuesta de Hello es Hola siguiendo el formato:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Ejemplo de la API de análisis**

**Solicitud**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Respuesta**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Operaciones del documento
En búsqueda de Azure, un índice se almacena en la nube de Hola y rellena con los documentos JSON que cargar toohello servicio. Todos los documentos de Hola que se cargan comprenden corpus de Hola de los datos de búsqueda. Los documentos contienen campos, algunos de los cuales se acortan en términos de búsqueda cuando se cargan. Hola `/docs` segmento de dirección URL en hello API de búsqueda de Azure representa la colección de Hola de documentos en un índice. Todas las operaciones realizadas en la colección de hello como cargar, combinar, eliminar o consultar documentos que tienen lugar en el contexto de Hola de un índice único, por lo que las direcciones de URL de Hola para estas operaciones siempre empezarán por `/indexes/[index name]/docs` para un nombre de índice especificado.

El código de aplicación debe generar JSON documentos tooupload tooAzure búsqueda o puede usar un [indizador](https://msdn.microsoft.com/library/dn946891.aspx) tooload documentos si el origen de datos de hello es la base de datos de SQL Azure o base de datos de Azure Cosmos. Normalmente, los índices se rellenan desde un único conjunto de datos que suministre.

Debe contar con un documento para cada elemento que desee toosearch. Una aplicación de alquiler de películas puede disponer de un documento por película, una aplicación de escaparate podría tener un documento por SKU, una aplicación de software con fines pedagógicos en línea podría tener un documento por curso, una empresa de investigación podría tener un documento para cada documento académico de su repositorio, y así sucesivamente.

Los documentos constan de uno o varios campos. Los campos pueden contener texto acortado por Búsqueda de Azure a términos de búsqueda, así como los valores no acortados o que no sean de texto que pueden utilizarse en filtros o perfiles de puntuación. Hello nombres, tipos de datos y características de búsqueda admitidas para cada campo se determinan por el esquema de índice Hola. Uno de los campos de hello en cada esquema de índice debe designarse como identificador, y cada documento debe tener un valor para el campo de Id. de Hola que identifica ese documento en el índice de Hola. Todos los demás campos de documento son opcionales y serán tooa de valor null si no se especifican. Tenga en cuenta que los valores null no ocupan espacio en el índice de búsqueda de Hola.

Antes de poder cargar documentos, debe ya ha creado el índice de hello en el servicio de Hola. Consulte [Crear índice](#CreateIndex) para obtener más información acerca de este primer paso.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Agregar, actualizar o eliminar documentos
Puede cargar, combinar, combinar o cargar o eliminar documentos en un índice especificado mediante HTTP POST. Para un gran número de actualizaciones, se recomienda el procesamiento por lotes de documentos (too1000 documentos por lote) o aproximadamente 16 MB por lote.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Puede cargar, combinar, combinar o cargar o eliminar documentos en un índice especificado mediante HTTP POST.

Hola URI de solicitud incluye [nombre del índice], especificar qué documentos de toopost de índice. Índice de tooone documentos sólo se puede registrar a la vez.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `Content-Type`: obligatorio. Establezca esta propiedad demasiado`application/json`
* `api-key`: obligatorio. Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **agregar documentos** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

cuerpo de saludo de solicitud de hello contiene uno o más toobe documentos indizados. Los documentos se identifican mediante una clave única. Cada documento está asociado a una acción: carga, combinación, combinación o carga o eliminación. Carga las solicitudes deben incluir los datos del documento Hola como un conjunto de pares clave/valor.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Las claves de documento solo pueden contener letras, números, guiones ("-"), caracteres de subrayado ("_") y signos igual ("="). Para obtener más información, consulte [Reglas de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Acciones de documentos**

* `upload`: Una acción de carga es similar tooan "upsert" donde se insertan si es nuevo y actualiza/reemplaza si existe el documento de Hola. Tenga en cuenta que todos los campos se reemplazan en caso de actualización de Hola.
* `merge`: Merge actualiza una existente de documentos con hello especifica campos. Si no existe el documento de hello, se producirá un error en la combinación de Hola. Cualquier campo que se especifica en una combinación reemplazará el campo existente de hello en el documento de Hola. Aquí se incluyen los campos de tipo `Collection(Edm.String)`. Por ejemplo, si hello documento contiene un campo "tags" con el valor `["budget"]` y ejecutar una combinación con el valor `["economy", "pool"]` para "etiquetas", valor final de Hola de campo Hola "tags" será `["economy", "pool"]`. **No** será `["budget", "economy", "pool"]`.
* `mergeOrUpload`: se comporta como `merge` si un documento con hello clave dada ya existe en el índice de Hola. Si el documento de hello no existe, ésta se comporta como `upload` con un nuevo documento.
* `delete`: La eliminación quita documento especificado Hola Hola índice. Tenga en cuenta que los campos especifique en una `delete` operación distinta de campo de clave de Hola se pasará por alto. Si desea tooremove un campo individual de un documento, use `merge` en su lugar y simplemente defina el campo de hello explícitamente demasiado`null`.

**Respuesta**

Código de estado: se obtendrá 200 Correcto con una respuesta correcta, lo que significa que todos los elementos se han indexado correctamente. Esto se indica mediante hello `status` propiedad se ha establecido tootrue para todos los elementos, así como hello `statusCode` propiedad se ha establecido tooeither 201 (para los documentos recién cargados) o 200 (para los documentos combinados o eliminados):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Se devolverá un código de estado 207 (varios estados) solo con que un elemento no se indexe correctamente. Elementos que no se han indizado tienen hello `status` toofalse de conjunto de campos. Hola `errorMessage` y `statusCode` propiedades indicará el motivo Hola Hola indización de error:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Hello en la tabla siguiente explica Hola distintos cada documento códigos de estado que se pueden devolver en la respuesta de Hola. Tenga en cuenta que algunos indican problemas con la solicitud de hello, mientras que otros usuarios indican condiciones de error temporal. Hola este último que debe reintentar después de un retraso.

<table style="font-size:12">
    <tr>
        <th>Código de estado</th>
        <th>Significado</th>
        <th>Se puede volver a intentar</th>
        <th>Notas</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Documento correctamente modificado o eliminado.</td>
        <td>N/D</td>
        <td>Las operaciones de eliminación son <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>. Es decir, incluso si una clave de documento no existe en el índice de hello, intentar una operación de eliminación con esa clave se producirá en un código de 200 estado.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>El documento se creó correctamente.</td>
        <td>N/D</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Se produjo un error en el documento de Hola que impidió que se está indizando.</td>
        <td>No</td>
        <td>mensaje de error de Hola en respuesta Hola indicará cuál es el problema con el documento de Hola.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>no se pudieron combinar documento Hola porque Hola clave dada no existe en el índice de Hola.</td>
        <td>No</td>
        <td>Este error no se produce durante las cargas ya que estas crean nuevos documentos y no se producen durante las eliminaciones porque son <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Se detectó un conflicto de versión al tratar de tooindex un documento.</td>
        <td>Sí</td>
        <td>Esto puede ocurrir al que está tratando de hello tooindex mismo documento más de una vez al mismo tiempo.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>índice de Hello no está disponible temporalmente porque se actualizó con allowIndexDowntime' hello' marca conjunto too'true'.</td>
        <td>Sí</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>El servicio de búsqueda no está disponible temporalmente, posiblemente debido a carga tooheavy.</td>
        <td>Sí</td>
        <td>El código debe esperar antes de reintentar en este caso, o se arriesga a prolongar la no disponibilidad del servicio de Hola.</td>
    </tr>
</table> 

**Tenga en cuenta**: si el código de cliente encuentra con frecuencia una respuesta 207, una razón posible es que sistema Hola está bajo carga. Puede confirmarlo comprobando hello `statusCode` propiedad 503. Si éste es el caso de hello, se recomienda ***la limitación de peticiones de indización***. En caso contrario, si el tráfico de indización no remite, el sistema de hello podría empezar a rechazar todas las solicitudes con 503 errores.

Código de estado 429 indica que se ha superado la cuota Hola número de documentos por índice. Debe crear un nuevo índice o actualizar para obtener límites de capacidad superiores.

**Ejemplo:**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Buscar documentos
A **búsqueda** operación se emite como una solicitud GET o POST y especifica los parámetros que proporcionen a los criterios de Hola para seleccionar documentos asociados.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Cuando este tipo de toouse en lugar de obtener**

Cuando se utiliza HTTP GET toocall hello **búsqueda** API, deberá toobe tenga en cuenta que longitud Hola de dirección URL de solicitud de hello no puede superar los 8 KB. Esto suele ser suficiente para la mayoría de las aplicaciones. Sin embargo, algunas aplicaciones generan consultas muy extensas o expresiones de filtro OData. Para estas aplicaciones, el uso de HTTP POST es una opción mejor porque permite filtros y consultas mayores que GET. Con POST, número de Hola de términos o cláusulas en una consulta está limitando Hola factor, no el tamaño de Hola de consulta sin procesar de hello como límite de tamaño de hello solicitud de POST es aproximadamente 16 MB.

> [!NOTE]
> Aunque el límite de tamaño de solicitud POST hello es muy grande, las consultas de búsqueda y las expresiones de filtro no pueden ser arbitrariamente complejas. Consulte la [sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx) y la [sintaxis de expresiones de OData](https://msdn.microsoft.com/library/dn798921.aspx) para más información sobre las limitaciones de complejidad de consultas y filtros de búsqueda.
> 
> 

**Solicitud**

HTTPS es necesario para las solicitudes de servicio. Hola **búsqueda** solicitud puede crearse mediante Hola GET o métodos POST.

URI de solicitud de Hello especifica qué tooquery de índice, para todos los documentos que coinciden con los parámetros de Hola. Se especifican en la cadena de consulta de hello en caso de hello de solicitudes GET, y en la solicitud de Hola solicita cuerpo en caso de hello de publicación.

Como práctica recomendada al crear las solicitudes GET, recuerde demasiado[codifica como URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parámetros cuando se llama a Hola API de REST directamente. Para las operaciones de **Búsqueda** , esto incluye:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

Solo se recomienda la codificación de direcciones URL en hello por encima de los parámetros de consulta. Si se codifica como URL accidentalmente hello cadena de consulta completa (todos los elementos después de hello?), se interrumpirán las solicitudes.

Además, la codificación de direcciones URL solo es necesaria cuando se llama a Hola obtener API de REST directamente mediante. Codificación de dirección URL no es necesaria cuando se llama a **búsqueda** mediante POST, o al usar hello [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que controla la codificación de direcciones URL para usted.

<a name="SearchQueryParameters"></a>
**Parámetros de consulta**

**búsqueda** acepta varios parámetros que ofrecen criterios de consulta y que también especifican el comportamiento de búsqueda. Proporcionar la cadena de consulta de estos parámetros en la dirección URL de hello al llamar a **búsqueda** a través de GET y como propiedades JSON en el cuerpo de la solicitud de hello al llamar a **búsqueda** a través de POST. sintaxis de Hola para algunos parámetros difiere ligeramente entre GET y POST. Estas diferencias se indican como aplicables a continuación:

`search=[string]`(opcional): Hola toosearch de texto para. Se busca en los campos `searchable` de forma predeterminada a menos que se especifique `searchFields`. Al buscar `searchable` se acorta campos, Hola texto de búsqueda, por lo que se pueden separar varios términos con espacios en blanco (por ejemplo: `search=hello world`). usar de cualquier término, toomatch `*` (puede ser útil para las consultas de filtro booleano). Si se omite este parámetro tiene el mismo efecto que si se establece demasiado de hello`*`. Vea [sintaxis de consulta Simple](https://msdn.microsoft.com/library/dn798920.aspx) para obtener información específica acerca de la sintaxis de búsqueda de Hola.

* **Tenga en cuenta**: resultados de Hola a veces pueden ser sorprendentes cuando se consulta sobre `searchable` campos. tokenizer Hola incluye lógica toohandle casos comunes tooEnglish texto como apóstrofo, comas en números, etcetera. Por ejemplo, `search=123,456` coincidirá con un término 123,456 en lugar de términos individuales de hello 123 y 456, dado que se utilizan comas como separadores de miles para números grandes en inglés. Por este motivo, se recomienda utilizar el espacio en blanco en lugar de términos de puntuación tooseparate Hola `search` parámetro.

`searchMode=any|all`(opcional, valor predeterminado es demasiado`any`): indica si alguno o todos los términos de búsqueda de hello deben coincidir en el documento de pedido toocount hello como una coincidencia.

`searchFields=[string]`(opcional): lista de Hola de toosearch de nombres de campo separados por comas para hello el texto especificado. Los campos de destino deben estar marcados como `searchable`.

`queryType=simple|full`(opcional, valor predeterminado es demasiado`simple`): cuando set demasiado "simple" Buscar texto se interpreta usando un lenguaje de consulta simple que permite símbolos como +, * y "". Las consultas se evalúan en todos los campos de búsqueda (o campos indicados en `searchFields`) en cada documento de manera predeterminada. Cuando se establece demasiado el tipo de consulta de hello`full` texto de búsqueda se interpreta con lenguaje de consulta de Lucene de Hola que permite realizar búsquedas específicas de los campos y ponderadas. Vea [sintaxis de consulta Simple](https://msdn.microsoft.com/library/dn798920.aspx) y [sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para obtener información específica sobre la sintaxis de búsqueda de Hola. 

> [!NOTE]
> Intervalo de búsqueda en hello Lucene no se admite el lenguaje de consulta en favor de $filter que ofrece una funcionalidad similar.
> 
> 

`moreLikeThis=[key]` (opcional) **Importante:**  esta característica solo está disponible en `2015-02-28-Preview`. Esta opción no se puede usar en una consulta que contiene el parámetro de búsqueda de texto hello, `search=[string]`. Hola `moreLikeThis` parámetro busca documentos que son similares documento toohello especificado por clave de documento de Hola. Cuando se realiza una solicitud de búsqueda con `moreLikeThis`, se genera una lista de términos de búsqueda en función de la frecuencia de Hola y escasez de términos en el documento de origen de Hola. Estos términos son utilizado toomake Hola solicitud. De forma predeterminada, Hola contenido de todos los `searchable` campos se consideran a menos que `searchFields` es toorestrict usa los campos que se buscan.  

`$skip=#`(opcional): número de Hola de búsqueda de resultados tooskip; No puede ser superior a 100 000. Si necesita tooscan documentos en secuencia pero no se puede usar `$skip` debido a la limitación toothis, considere el uso de `$orderby` en una clave totalmente ordenada y `$filter` con un intervalo de consulta en su lugar.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `skip` en lugar de `$skip`.
> 
> 

`$top=#`(opcional): número de Hola de búsqueda resultados tooretrieve. Esto puede utilizarse junto con `$skip` tooimplement paginación por parte del cliente de resultados de la búsqueda.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `top` en lugar de `$top`.
> 
> 

`$count=true|false`(opcional, valor predeterminado es demasiado`false`)-especifica si toofetch Hola número total de resultados. Es Hola recuento de todos los documentos que coinciden con hello `search` y `$filter` parámetros, se omitirá `$top` y `$skip`. Este valor demasiado`true` puede afectar al rendimiento. Tenga en cuenta que devuelve el recuento de hello es una aproximación.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `count` en lugar de `$count`.
> 
> 

`$orderby=[string]`(opcional): una lista de expresiones separadas por comas toosort Hola resultados por. Cada expresión puede ser un nombre de campo o una llamada toohello `geo.distance()` función. Cada expresión puede ir seguida de `asc` tooindicated ascendente, y `desc` tooindicate descendente. valor predeterminado de Hello es ascendente. El empate se rompe por las puntuaciones de coincidencia de Hola de documentos. Si no hay ningún `$orderby` se especifica, criterio de ordenación predeterminado de hello es descendente según la puntuación de coincidencia de documento. Hay un límite de 32 cláusulas para `$orderby`.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `orderby` en lugar de `$orderby`.
> 
> 

`$select=[string]`(opcional): una lista de campos separados por comas tooretrieve. Si no se especifica, se incluyen todos los campos marcados como recuperables en el esquema de Hola. Puede solicitar explícitamente todos los campos, establezca este parámetro demasiado`*`.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `select` en lugar de `$select`.
> 
> 

`facet=[string]`(cero o más) - un toofacet campo por. Opcionalmente, Hola de cadena puede contener facetas de parámetros toocustomize Hola expresado como separada por comas `name:value` pares. Los parámetros válidos son:

* `count` (número máximo de términos de faceta; el valor predeterminado es 10). No hay ningún máximo, pero los valores más altos incurren en una disminución correspondiente del rendimiento, especialmente si el campo por facetas hello contiene un gran número de términos únicos.
  * Por ejemplo: `facet=category,count:5` obtiene Hola cinco categorías principales en los resultados de la faceta.  
  * **Tenga en cuenta**: si hello `count` parámetro es menor que el número de Hola de términos únicos, resultados de hello pueden no ser exacto. Esto es debido a las consultas de facetas se distribuyen entre las particiones de forma de toohello. Aumentar `count` generalmente aumenta Hola precisión de recuentos de término de hello, pero con un costo de rendimiento.
* `sort`(una de `count` toosort *descendente* por número, `-count` toosort *ascendente* por número, `value` toosort *ascendente* por valor, o `-value` toosort *descendente* por valor)
  * Por ejemplo: `facet=category,count:3,sort:count` obtiene Hola tres categorías principales en los resultados de la faceta en orden descendente por número de Hola de documentos con cada nombre de ciudad. Por ejemplo, si tres categorías principales Hola son presupuesto, Motel y lujo y presupuesto tiene 5 resultados, Motel tiene 6 y lujo tiene 4, a continuación, hello depósitos será en orden de hello Motel, presupuesto, lujo.
  * Por ejemplo: `facet=rating,sort:-value` genera depósitos para todas las clasificaciones posibles en orden descendente por valor. Por ejemplo, si las clasificaciones de hello son de 1 too5, Hola cubos se ordenarán 5, 4, 3, 2, 1, independientemente de cuántos documentos coinciden con cada clasificación.
* `values` (valores numéricos delimitados por canalización o `Edm.DateTimeOffset` que especifican un conjunto dinámico de valores de entrada de faceta)
  * Por ejemplo: `facet=baseRate,values:10|20` genera tres cubos: uno para la tarifa base 0 seguridad toobut sin incluir 10, uno para 10 arriba toobut sin incluir 20 y uno para 20 o superior.
  * Por ejemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` genera dos depósitos: uno para hoteles reformados antes de febrero de 2010 y otro para hoteles reformados desde el 1 de febrero de 2010 en adelante.
* `interval` (intervalo de número entero mayor que 0 para números, o `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para los valores de fecha y hora)
  * Por ejemplo: `facet=baseRate,interval:100` genera depósitos basados en intervalos de tarifas base de tamaño de 100. Por ejemplo, si las tarifas base se encuentran entre 60 y 600 dólares, habrá depósitos para 0-100, 100-200, 300 200, 300-400, 400-500 y 500-600.
  * Por ejemplo: `facet=lastRenovationDate,interval:year` genera un depósito para cada año en que se han reformado los hoteles.
* `timeoffset` ([+-] hh: mm, [+-] hhmm, o [+-] hh) `timeoffset` es opcional. Solo puede combinarse con hello `interval` opción y sólo cuando aplica tooa campo de tipo `Edm.DateTimeOffset`. valor de Hello especifica tooaccount desplazamiento de hora UTC hello para establecer los límites de tiempo.
  * Por ejemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa Hola límites de día que empieza en 01:00:00 UTC (medianoche en la zona horaria de destino de hello)
* **Tenga en cuenta**: `count` y `sort` se pueden combinar en hello misma especificación de faceta, pero no se puede combinar con `interval` o `values`, y `interval` y `values` no se pueden combinar entre sí.
* **Nota**: Las facetas de intervalo de fecha y hora se calculan en función de la hora UTC si `timeoffset` no se ha especificado. Por ejemplo: para `facet=lastRenovationDate,interval:day`, límites de día de hello comienza en 00:00:00 UTC. 

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `facets` en lugar de `facet`. Además, lo especifica como una matriz JSON de cadenas, donde cada cadena es una expresión de faceta independiente.
> 
> 

`$filter=[string]` (opcional): expresión de búsqueda estructurada en la sintaxis estándar de OData.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `filter` en lugar de `$filter`.
> 
> 

`highlight=[string]` (opcional): conjunto de nombres de campos delimitado por comas usado para los resaltados de referencias. Solo se pueden usar `searchable` campos para resaltar las referencias.

`highlightPreTag=[string]`(opcional, valor predeterminado es demasiado`<em>`): una cadena de etiqueta que se antepone toohit resaltados. Debe establecerse con `highlightPostTag`.

> [!NOTE]
> Al llamar a **búsqueda** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).
> 
> 

`highlightPostTag=[string]`(opcional, valor predeterminado es demasiado`</em>`)-una etiqueta de cadena que se anexa información destacada de toohit. Debe establecerse con `highlightPreTag`.

> [!NOTE]
> Al llamar a **búsqueda** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).
> 
> 

`scoringProfile=[string]`(opcional): nombre Hola de una puntuación tooevaluate perfil puntuaciones de coincidencia para documentos coincidentes en los resultados de orden toosort Hola.

`scoringParameter=[string]`(cero o más): indican los valores de hello para cada parámetro definido en una función de puntuación (por ejemplo, `referencePointParameter`) con formato de hello `name-value1,value2,...`.

* Por ejemplo, si Hola perfil de puntuación define una función con un parámetro llamado "mylocation" opción de la cadena de consulta de hello sería `&scoringParameter=mylocation--122.2,44.8`. guión primera Hola separa el nombre de Hola de lista de valores de hello, mientras guión segundo Hola forma parte del primer valor de hello (longitud en este ejemplo).
* Para los parámetros de puntuación como etiqueta de impulso puede contener comas, puede omitir cualquier tales valores de lista de hello con comillas simples. Si los propios valores de hello contengan comillas simples, se puede omitir duplicando.
  * Por ejemplo, si tiene una etiqueta impulso parámetro denominado "mytag" y desea tooboost en etiqueta Hola valores "¡Hello, o ' Brien" y "Smith", consulta Hola cadena opción sería `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Tenga en cuenta que las comillas solo son necesarias para los valores que contienen comas.

> [!NOTE]
> Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `scoringParameters` en lugar de `scoringParameter`. Además, lo especifica como una matriz JSON de cadenas, donde cada cadena es un par `name-values` independiente.
> 
> 

`minimumCoverage`(opcional, tiene como valor predeterminado too100) - un número entre 0 y 100 que indica el porcentaje de Hola de índice de Hola que debe ser abarcado por una consulta de búsqueda en orden para hello consulta toobe notificarse como tales. De forma predeterminada, todo índice de hello debe estar disponible o `Search` se devolverá el código de estado HTTP 503. Si establece `minimumCoverage` y `Search` se realiza correctamente, devolverá HTTP 200 e incluyen una `@search.coverage` valor de respuesta de Hola que indica el porcentaje de Hola de índice de Hola que se incluyó en la consulta de Hola.

> [!NOTE]
> Establecer este valor de parámetro tooa menor que 100 puede ser útil para garantizar la disponibilidad de búsqueda incluso para servicios con una única réplica. Sin embargo, no todos los documentos coincidentes se garantiza que toobe presente en los resultados de búsqueda de Hola. Si la recuperación de búsqueda es más importante aplicación tooyour de disponibilidad, es mejor tooleave `minimumCoverage` en su valor predeterminado de 100.
> 
> 

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

Nota: Para realizar esta operación, Hola `api-version` se especifica como un parámetro de consulta de dirección URL de hello independientemente de si se llama a **búsqueda** con GET o POST.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena único tooyour dirección URL del servicio. Hola **búsqueda** solicitud puede especificar una clave de administración o la clave de consulta para `api-key`.

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Para GET: ninguno.

Para POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Continuación de las respuestas de búsqueda parciales**

A veces, búsqueda de Azure no puede devolver que todos los Hola resultados solicitados en una única respuesta de búsqueda. Esto puede ocurrir por diferentes motivos, como consultas de hello las solicitudes de demasiados documentos especificando no `$top` o especificar un valor para `$top` que es demasiado grande. En tales casos, búsqueda de Azure incluirá hello `@odata.nextLink` anotación en el cuerpo de la respuesta de hello y también `@search.nextPageParameters` si era una solicitud POST. Puede usar valores de hello de estas anotaciones tooformulate otra búsqueda solicitud tooget Hola siguiente parte de la respuesta de la búsqueda de Hola. Esto se denomina una ***continuación*** de solicitud de búsqueda original de Hola y Hola generalmente se denominan anotaciones ***tokens de continuación***. Vea [ejemplo Hola siguiente](#SearchResponse) para obtener más información acerca de la sintaxis de Hola de estas anotaciones y que aparecen en el cuerpo de la respuesta de Hola. 

¿Por qué la búsqueda de Azure podría devolver tokens de continuación de razones de Hello son toochange específico de la implementación y está sujeto. Los clientes sólidos siempre deben ser toohandle listo casos donde se devuelven documentos menos de lo esperado y un token de continuación es toocontinue incluye la recuperación de documentos. También tenga en cuenta que debe usar Hola mismo método HTTP como solicitud original de hello en orden toocontinue. Por ejemplo, si envía una solicitud GET, las solicitudes de continuación que envíe también deben utilizar GET (y lo mismo para POST).

<a name="SearchResponse"></a>
**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Ejemplos:**

Puede encontrar ejemplos adicionales en hello [sintaxis de expresiones de OData para búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) página.

1)    Hola de búsqueda índice descendente por fecha.

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    En una búsqueda por facetas, busque en el índice de Hola y recupere facetas para categorías, clasificación, etiquetas, así como elementos con baseRate en intervalos específicos:

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    Mediante un filtro, restringir los resultados de consulta por facetas anterior Hola después Hola usuario hace clic en clasificación 3 y la categoría "Motel":

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) En una búsqueda con facetas, establezca un límite superior en términos únicos devueltos en una consulta. valor predeterminado de Hello es 10, pero puede aumentar o disminuir este valor mediante hello `count` parámetro en hello `facet` atributo:

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    Hola índice de búsqueda en campos específicos; Por ejemplo, un campo específico del idioma:

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) Buscar Hola índice en varios campos. Por ejemplo, puede almacenar y campos de consulta de búsqueda en varios idiomas, todo dentro de Hola mismo índice.  Si las descripciones de inglés y francés coexisten en hello mismo documento, puede devolver hello en uno o todos los resultados de la consulta:

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

Tenga en cuenta que solo puede consultar un índice de cada vez. No cree varios índices para cada idioma a menos que piense tooquery uno a la vez.

7)    Paginación: página 1 de Get hello de elementos (el tamaño de página es 10):

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    Paginación: página 2 º de Get hello de elementos (el tamaño de página es 10):

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    Recupere un conjunto específico de campos:

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  Recupere documentos que coincidan con una expresión de filtro específica:

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) Busque en el índice de Hola y devolver fragmentos con resultados destacados

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) Busque en el índice de Hola y devuelva documentos ordenados desde más de cerca toofarther fuera de una ubicación de referencia

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) Búsqueda Hola índice suponiendo que existe es un perfil de puntuación llamado "geo" con dos funciones de puntuación de distancia, uno define un parámetro llamado "currentLocation" y otro que define un parámetro llamado "lastLocation"

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) Buscar documentos en hello índice utilizando [sintaxis de consulta simple](https://msdn.microsoft.com/library/dn798920.aspx). Esta consulta devuelve hoteles donde los campos que permiten búsqueda contienen Hola términos "comodidad" y "ubicación" pero no "motel":

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

Tenga en cuenta uso Hola de `searchMode=all` anteriormente. Incluir este parámetro invalida el valor predeterminado de Hola de `searchMode=any`, lo que asegura que `-motel` significa "AND NOT" en lugar de "OR NOT". Sin `searchMode=all`, obtendrá "OR NOT" que se expande en lugar de restringe los resultados de búsqueda, y puede ser contraproducente toosome a los usuarios.

15) Buscar documentos en hello índice utilizando [sintaxis de consulta de lucene](https://msdn.microsoft.com/library/mt589323.aspx). Esta consulta devuelve hoteles donde el campo de categoría hello contiene Hola término "budget" y puede buscar todos los campos que contengan la frase Hola "renovada recientemente". Documentos que contengan la frase Hola "recientemente reformada" con un rango superior como resultado del valor de aumento de término de hello (3)

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Buscar documento
Hola **búsqueda de documento** operación recupera un documento de búsqueda de Azure. Esto es útil cuando un usuario hace clic en un resultado de búsqueda específico y desea toolook detalles concretos de ese documento.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Solicitud**

HTTPS es necesario para las solicitudes de servicio. Hola **búsqueda de documento** solicitud se puede generar como sigue.

    GET /indexes/[index name]/docs/key?[query parameters]

Como alternativa, puede usar la sintaxis de OData tradicional de Hola para búsqueda de claves:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Hola URI de solicitud incluye un [nombre de índice] y [key], especificar qué tooretrieve documento desde qué índice. Solamente se puede obtener un documento de cada vez. Use **búsqueda** tooget varios documentos en una sola solicitud.

**Parámetros de consulta**

`$select=[string]`(opcional): una lista de campos separados por comas tooretrieve. Si no se especifica o se establece demasiado`*`, se incluyen todos los campos marcados como recuperables en el esquema de hello en proyección Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

Nota: Para realizar esta operación, Hola `api-version` se especifica como un parámetro de consulta.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena único tooyour dirección URL del servicio. Hola **búsqueda de documento** solicitud puede especificar una clave de administración o la clave de consulta para `api-key`.

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Ninguno.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Ejemplo**

Documento de Hola de búsqueda que tiene la clave '2'

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Documento de Hola de búsqueda que tiene la clave "3" utilizando la sintaxis de OData:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Documentos de recuento
Hola **número de documentos** operación recupera un recuento del número de Hola de documentos en un índice de búsqueda. Hola `$count` sintaxis forma parte del programa Hola Protocolo OData.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Solicitud**

HTTPS es necesario para las solicitudes de servicio. Hola **número de documentos** solicitud puede crearse mediante el método GET de Hola.

Hola [nombre del índice] en el URI de solicitud de hello indica Hola servicio tooreturn un recuento de todos los elementos de colección de documentos de Hola de índice especificado de Hola.

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.

* `Accept`: Este valor debe estar establecido demasiado`text/plain`.
* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena único tooyour dirección URL del servicio. Hola **número de documentos** solicitud puede especificar una clave de administración o la clave de consulta para `api-key`.

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Ninguno.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

cuerpo de respuesta de Hello contiene el valor del recuento de Hola como un entero con formato de texto sin formato.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Sugerencias
Hola **sugerencias** operación recupera sugerencias basadas en la entrada de búsqueda parcial. Normalmente se utiliza en cuadros tooprovide anticipada sugerencias como los usuarios están escribiendo términos de búsqueda.

Solicitudes de sugerencias tienen como fin sugerir documentos de destino, para que hello sugiere texto puede repetirse si varios documentos candidatos coinciden Hola mismo Buscar entrada. Puede usar `$select` tooretrieve otro documento campos (incluida la clave de documento de hello) por lo que puede indicarle qué documento es el origen de Hola para cada sugerencia.

Una operación **Sugerencias** se emite como una solicitud GET o POST.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Cuando este tipo de toouse en lugar de obtener**

Cuando se utiliza HTTP GET toocall hello **sugerencias** API, deberá toobe tenga en cuenta que longitud Hola de dirección URL de solicitud de hello no puede superar los 8 KB. Esto suele ser suficiente para la mayoría de las aplicaciones. Sin embargo, algunas aplicaciones generan consultas muy extensas, en concreto, expresiones de filtro de OData. Para estas aplicaciones, el uso de HTTP POST es una opción mejor porque permite filtros mayores que GET. Utiliza el método POST, número Hola de cláusulas de un filtro es el factor de limitación de hello, no Hola tamaño de la cadena de filtro sin procesar de hello como límite de tamaño de hello solicitud de POST es aproximadamente 16 MB.

> [!NOTE]
> Aunque el límite de tamaño de solicitud POST hello es muy grande, las expresiones de filtro no pueden ser arbitrariamente complejas. Consulte [Sintaxis de expresiones de OData para Búsqueda de Azure](https://msdn.microsoft.com/library/dn798921.aspx) para obtener más información sobre las limitaciones de complejidad de filtros.
> 
> 

**Solicitud**

HTTPS es necesario para las solicitudes de servicio. Hola **sugerencias** solicitud puede crearse mediante Hola GET o métodos POST.

URI de solicitud de Hello especifica nombre de Hola de hello tooquery de índice. Se especifican parámetros, como término de búsqueda escrito parcialmente de hello, en la cadena de consulta de hello en caso de hello de solicitudes GET y, en la solicitud de hello solicita cuerpo en caso de hello de publicación.

Como práctica recomendada al crear las solicitudes GET, recuerde demasiado[codifica como URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parámetros cuando se llama a Hola API de REST directamente. Para las operaciones **Sugerencias** , se incluye lo siguiente:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

Solo se recomienda la codificación de direcciones URL en hello por encima de los parámetros de consulta. Si se codifica como URL accidentalmente hello cadena de consulta completa (todos los elementos después de hello?), se interrumpirán las solicitudes.

Además, la codificación de direcciones URL solo es necesaria cuando se llama a Hola obtener API de REST directamente mediante. Codificación de dirección URL no es necesaria cuando se llama a **sugerencias** mediante POST, o al usar hello [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que controla la codificación de direcciones URL para usted.

**Parámetros de consulta**

**Sugerencias** acepta varios parámetros que ofrecen criterios de consulta y que también especifican el comportamiento de búsqueda. Proporcionar la cadena de consulta de estos parámetros en la dirección URL de hello al llamar a **sugerencias** a través de GET y como propiedades JSON en el cuerpo de la solicitud de hello al llamar a **sugerencias** a través de POST. sintaxis de Hola para algunos parámetros difiere ligeramente entre GET y POST. Estas diferencias se indican como aplicables a continuación:

`search=[string]`-Hola toouse toosuggest consultas de búsqueda de texto. Debe tener 1 carácter como mínimo y no más de 100 caracteres.

`highlightPreTag=[string]`(opcional): una etiqueta de cadena que se antepone toosearch aciertos. Debe establecerse con `highlightPostTag`.

> [!NOTE]
> Al llamar a **sugerencias** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).
> 
> 

`highlightPostTag=[string]`(opcional): una etiqueta de cadena que se anexa toosearch aciertos. Debe establecerse con `highlightPreTag`.

> [!NOTE]
> Al llamar a **sugerencias** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).
> 
> 

`suggesterName=[string]`-nombre de hello del proveedor de sugerencias de hello como Hola especificado en `suggesters` colección que forma parte de la definición del índice Hola. Un `suggester` determina qué campos se analizan para encontrar términos de consulta sugeridos. Consulte [Proveedores de sugerencias](#Suggesters) para obtener más información.

`fuzzy=[boolean]`(opcional, el valor predeterminado = false)-tootrue cuando se establece esta API encontrará sugerencias incluso si hay un carácter sustituye o falta en el texto de búsqueda de Hola. Si bien esto proporciona una mejor experiencia en algunos escenarios, ello afecta al rendimiento, ya que las búsquedas de sugerencias aproximadas son más lentas y consumen más recursos.

`searchFields=[string]`(opcional): lista de Hola de toosearch de nombres de campo separados por comas para hello especifica el texto de búsqueda. Los campos de destino deben estar habilitados para obtener sugerencias.

`$top=#`(opcional, el valor predeterminado = 5)-número de sugerencias tooretrieve de Hola. Debe ser un número entre 1 y 100.

> [!NOTE]
> Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `top` en lugar de `$top`.
> 
> 

`$filter=[string]`(opcional): una expresión que filtra los documentos de hello considerados para obtener sugerencias.

> [!NOTE]
> Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `filter` en lugar de `$filter`.
> 
> 

`$orderby=[string]`(opcional): una lista de expresiones separadas por comas toosort Hola resultados por. Cada expresión puede ser un nombre de campo o una llamada toohello `geo.distance()` función. Cada expresión puede ir seguida de `asc` tooindicated ascendente, y `desc` tooindicate descendente. valor predeterminado de Hello es ascendente. Hay un límite de 32 cláusulas para `$orderby`.

> [!NOTE]
> Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `orderby` en lugar de `$orderby`.
> 
> 

`$select=[string]`(opcional): una lista de campos separados por comas tooretrieve. Si no se especifica, solo Hola clave de documento y se devuelve el texto de sugerencia. Puede solicitar explícitamente todos los campos, establezca este parámetro demasiado`*`.

> [!NOTE]
> Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `select` en lugar de `$select`.
> 
> 

`minimumCoverage`(opcional, tiene como valor predeterminado too80) - un número entre 0 y 100 que indica el porcentaje Hola de índice de Hola que debe ser abarcado por una consulta de sugerencias en orden para hello consulta toobe notificarse como tales. De forma predeterminada, debe estar disponible al menos el 80% del índice de Hola o `Suggest` se devolverá el código de estado HTTP 503. Si establece `minimumCoverage` y `Suggest` se realiza correctamente, devolverá HTTP 200 e incluyen una `@search.coverage` valor de respuesta de Hola que indica el porcentaje de Hola de índice de Hola que se incluyó en la consulta de Hola.

> [!NOTE]
> Establecer este valor de parámetro tooa menor que 100 puede ser útil para garantizar la disponibilidad de búsqueda incluso para servicios con una única réplica. Sin embargo, no todas las sugerencias de búsqueda de coincidencias se garantiza que toobe presente en los resultados de Hola. Si la recuperación es más importante aplicación de tooyour de disponibilidad, entonces es mejor no toolower `minimumCoverage` por debajo de su valor predeterminado de 80.
> 
> 

`api-version=[string]` (obligatorio). versión de vista previa de Hello es `api-version=2015-02-28-Preview`. Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.

Nota: Para realizar esta operación, Hola `api-version` se especifica como un parámetro de consulta de dirección URL de hello independientemente de si se llama a **sugerencias** con GET o POST.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales

* `api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena único tooyour dirección URL del servicio. Hola **sugerencias** solicitud puede especificar una clave de administración o la clave de consulta como hello `api-key`.

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

**Cuerpo de la solicitud**

Para GET: ninguno.

Para POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Si es de opción de proyección de hello tooretrieve usado campos se incluyen en cada elemento de matriz de hello:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Ejemplo**

Recuperar 5 sugerencias donde hello entrada de búsqueda parcial es 'lux'

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
