---
title: "perfiles de aaaScoring (búsqueda REST API versión 2015-02-28-vista previa de Azure) | Documentos de Microsoft"
description: "Búsqueda de Azure es un servicio de búsqueda hospedado en la nube que admite la optimización de resultados basados en perfiles de puntuación definidos por el usuario."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Perfiles de puntuación (API de REST de Búsqueda de Azure: 2015-02-28-Preview)
> [!NOTE]
> Este artículo describen los perfiles de puntuación en hello [vista previa 2015-02-28](search-api-2015-02-28-preview.md). Actualmente no hay ninguna diferencia entre hello `2016-09-01` versión documentados en [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) hello y `2015-02-28-Preview` versión se describe aquí, pero ofrecemos este documento todas formas en la cobertura de documento de pedido tooprovide a través de Hola API completa.
>
>

## <a name="overview"></a>Información general
La puntuación hace referencia toohello cálculo de una puntuación de búsqueda para todos los elementos devueltos en los resultados de búsqueda. puntuación de Hello es un indicador de relevancia de un elemento en el contexto de Hola de operación de búsqueda actual de Hola. Hola mayor puntuación hello, Hola artículo de hello más relevante. En los resultados de búsqueda, los elementos están ordenados de toolow alta, en función de puntuación de búsqueda de hello calcula para cada elemento.

Búsqueda de Azure usa la puntuación toocompute una puntuación inicial predeterminada, pero puede personalizar el cálculo de Hola a través de un perfil de puntuación. Perfiles de puntuación ofrecen mayor control sobre la clasificación de Hola de los elementos en los resultados de búsqueda. Por ejemplo, podría desea elementos tooboost según su potencial de ingresos, promover elementos más recientes o quizás aumentar elementos que han permanecido en inventario demasiado largo.

Un perfil de puntuación forma parte de la definición del índice hello, consta de campos, funciones y parámetros.

toogive se haga una idea del aspecto de un perfil de puntuación como hello en el ejemplo siguiente se muestra un perfil simple denominado "geo". Éste aumenta los elementos que tengan el término de búsqueda de Hola Hola `hotelName` campo. También usa hello `distance` función toofavor elementos que están dentro de diez kilómetros de la ubicación actual de Hola. Si alguien busca Hola término "inn" y "inn" ocurre toobe parte del nombre del hotel hello, documentos que incluyan hoteles con "inn" aparecerán mayores en resultados de búsqueda de Hola.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

toouse que este perfil de puntuación, la consulta es Formula toospecify perfil de hello en la cadena de consulta de Hola. En la siguiente consulta de hello, observe el parámetro de consulta de hello, `scoringProfile=geo` en solicitud de saludo.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Esta consulta busca Hola término "inn" y se pasa en la ubicación actual de Hola. Tenga en cuenta que esta consulta incluye otros parámetros, como `scoringParameter`. Los parámetros de consulta se describen en [Buscar documentos (API de Búsqueda de Azure)](search-api-2015-02-28-preview.md#SearchDocs).

Haga clic en [ejemplo](#example) tooreview un ejemplo más detallado de un perfil de puntuación.

## <a name="what-is-default-scoring"></a>¿Qué es la puntuación predeterminada?
La puntuación calcula una puntuación de la búsqueda para cada elemento de un conjunto de resultados ordenado por rango. Todos los elementos de un conjunto de resultados de búsqueda se asigna una puntuación de búsqueda, a continuación, el rango más alto toolowest. Se devuelven los elementos con las puntuaciones más altas hello toohello aplicación. De forma predeterminada, hello 50 mejores se devuelven, pero puede usar hello `$top` parámetro tooreturn un número mayor o menor de elementos (arriba too1000 en una única respuesta).

De forma predeterminada, una puntuación de búsqueda se calcula en función de propiedades estadísticas de consultas de Hola y los datos de Hola. Búsqueda de Azure busca documentos que contengan los términos de búsqueda de hello en la cadena de consulta de hello (algunas o todas, dependiendo de `searchMode`), dando prioridad a los documentos que contienen muchas instancias del término de búsqueda de Hola. puntuación de búsqueda de Hello aumenta incluso superior si término hello es poco frecuente en los corpus de datos de hello, pero común dentro del documento de Hola. base de Hola para una relevancia de toocomputing de este enfoque se conoce como TF IDF o (frecuencia de término frecuencia inversa de documento).

Suponiendo que no hay ninguna ordenación personalizada, los resultados se clasifican por puntuación de búsqueda antes de que se devuelvan toohello de aplicación que llama. Si `$top` no se especifica, 50 elementos de búsqueda de hello mayor puntuación se devuelve.

Los valores de puntuación de búsqueda pueden repetirse a lo largo de un conjunto de resultados. Por ejemplo, puede tener 10 elementos con una puntuación de 1,2, 20 elementos con una puntuación de 1,0 y 20 elementos con una puntuación de 0,5. Cuando varios resultados ha hello misma puntuación de búsqueda, Hola orden de los mismos elementos con puntuación no está definido y no es estable. Vuelva a ejecutar la consulta de Hola y es posible que vea posición de desplazamiento de elementos. Si dos elementos disponen de la misma puntuación, no hay ninguna garantía de cuál aparecerá en primer lugar.

## <a name="when-toouse-custom-scoring"></a>Cuando la puntuación personalizada toouse
Debe crear uno o varios perfiles de puntuación al comportamiento de clasificación predeterminado de hello no vaya cumplir lo suficiente en sus objetivos empresariales. Por ejemplo, podría decidir que la relevancia de la búsqueda debe favorecer a los elementos recién agregados. Asimismo, podría tener un campo que contenga el margen de beneficio, o algún otro campo que indique los ingresos potenciales. Incremento de los resultados que ofrecen beneficios tooyour empresarial puede ser un factor importante en decidir toouse los perfiles de puntuación.

El orden basado en relevancia también se implementa a través de perfiles de puntuación. Considere la posibilidad de resultados de búsqueda de páginas que usó en hello anterior que permiten ordenación por precio, fecha, clasificación o relevancia. En la búsqueda de Azure, perfiles de puntuación impulsan la opción de "relevancia" Hola. definiciones de Hola de relevancia es controlado por el usuario, se basa en los objetivos de negocio y el tipo de Hola de experiencia de búsqueda que desee toodeliver.

<a name="example"></a>

## <a name="example"></a>Ejemplo
Tal y como se ha indicado, la puntuación personalizada se implementa mediante los perfiles de puntuación definidos en un esquema de índice.

En este ejemplo se muestra hello esquema de un índice con dos perfiles de puntuación (`boostGenre`, `newAndHighlyRated`). Las consultas sobre este índice que incluyan cualquier perfil como un parámetro de consulta utilizarán el conjunto de resultados de hello perfil tooscore Hola.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Flujo de trabajo
tooimplement personalizado la puntuación del comportamiento, agregue un esquema de toohello perfil de puntuación que define el índice de Hola. Puede tener hasta los perfiles de puntuación too16 dentro de un índice (consulte [límites de servicio](search-limits-quotas-capacity.md)), pero solo se puede especificar un perfil en tiempo en una consulta concreta.

Iniciar con hello [plantilla](#bkmk_template) proporcionados en este tema.

Proporcione un nombre. Los perfiles de puntuación son opcionales, pero si agrega uno, se requiere nombre de Hola. Ser seguro toofollow convenciones de nomenclatura de Hola para campos (empiece con una letra, evite caracteres especiales y palabras reservadas). Consulte [Reglas de nomenclatura](http://msdn.microsoft.com/library/azure/dn857353.aspx) para obtener más información.

cuerpo de Hola de hello perfil de puntuación se construye desde funciones y campos ponderados.

### <a name="weights"></a>Pesos
Hola `weights` propiedad de un perfil de puntuación especifica los pares de nombre / valor que asignar un campo de tooa de peso relativo. Hola [ejemplo](#example), campos de álbum, género y nombre de artista Hola son impulsados 1.5, 5 y 2, respectivamente. ¿Por qué género aumenta mucho más alto de Hola a otros usuarios? Si se realiza la búsqueda sobre datos que son un poco homogéneos (como sucede Hola de "género" Hola `musicstoreindex`), es posible que tenga una mayor variación en ponderaciones relativas de Hola. Por ejemplo, en hello `musicstoreindex`, "rock" aparece como género y en las descripciones de género expresadas de forma idéntica. Si desea que la descripción de género toooutweigh género, el campo de género Hola necesitará una ponderación relativa mucho mayor.

### <a name="functions"></a>Functions
Funciones usadas cuando se requieren cálculos adicionales para contextos concretos. Los tipos de función válidos son `freshness`, `magnitude`, `distance` y `tag`. Cada función tiene parámetros que son tooit único.

* `freshness`debe utilizarse cuando desea es tooboost por lo novedoso o antiguo de un elemento. Esta función solo puede usarse con campos datetime (`Edm.DataTimeOffset`). Hola Nota `boostingDuration` atributo se utiliza sólo con la función de actualización de Hola.
* `magnitude`debe utilizarse cuando desea es tooboost en función de cómo alto o bajo un valor numérico. Entre los escenarios que requieren esta función se incluyen aumentar por margen de beneficio, precio máximo, precio mínimo o recuento de descargas. Puede invertir intervalo hello, toolow alta, si desea que el patrón inverso hello (por ejemplo, tooboost artículos de menor precio más de mayor precio). Debido a un intervalo de precios de 100 $ demasiado$ 1, se establecería `boostingRangeStart` en 100 y `boostingRangeEnd` en elementos de menor precio de 1 tooboost Hola. Esta función solo puede usarse con campos doble y de número entero.
* `distance`debe utilizarse cuando se desea tooboost por proximidad o ubicación geográfica. Esta función solo puede usarse con campos `Edm.GeographyPoint` .
* `tag`debe utilizarse cuando se desea tooboost por etiquetas en común entre documentos y consultas de búsqueda. Esta función solo puede usarse con campos `Edm.String` y `Collection(Edm.String)`.

#### <a name="rules-for-using-functions"></a>Reglas de uso de funciones
* El tipo de función (actualización, magnitud, distancia, etiqueta) debe aparecer en minúsculas.
* Las funciones no pueden incluir valores nulos ni estar vacías. En concreto, si incluye fieldname, tiene tooset lo toosomething.
* Las funciones sólo pueden ser campos de toofilterable aplicado. Consulte [Crear índice](search-api-2015-02-28-preview.md#CreateIndex) para más información sobre los campos que se pueden filtrar.
* Las funciones solo pueden ser aplicados toofields que se definen en la colección de campos de Hola de un índice.

Una vez definido el índice de hello, generar el índice de hello mediante la carga de esquema de índice de hello, seguido de documentos. Consulte [Crear índice](search-api-2015-02-28-preview.md#CreateIndex) y [Agregar, actualizar o eliminar documentos](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) para obtener instrucciones sobre estas operaciones. Una vez que se genera el índice de hello, debe tener un perfil de puntuación funcional que funciona con los datos de búsqueda.

<a name="bkmk_template"></a>

## <a name="template"></a>Plantilla
Esta sección muestra la sintaxis de Hola y la plantilla para los perfiles de puntuación. Consulte demasiado[referencia de los atributos de índice](#bkmk_indexref) en la siguiente sección para obtener descripciones de los atributos de Hola de Hola.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
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
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Referencia de propiedad de perfil de puntuación
> [!NOTE]
> Una función de puntuación solo puede ser aplicados toofields filtrables.
>
>

| Propiedad | Description |
| --- | --- |
| `name` |Necesario. Este es el nombre de Hola de hello perfil de puntuación. Se sigue Hola mismas convenciones de nomenclatura de un campo. Debe empezar por una letra y no puede contener puntos, signos de dos puntos ni símbolos @ y no se puede iniciar con la frase de Hola "azureSearch" (distingue mayúsculas de minúsculas). |
| `text` |Contiene la propiedad de pesos de Hola. |
| `weights` |Opcional. Par de nombre-valor que especifica un nombre de campo y un peso relativo. El peso relativo debe ser un número entero positivo o un número de punto flotante. Puede especificar el nombre del campo Hola sin una ponderación correspondiente. Pesos son utilizados tooindicate Hola importancia de tooanother relativa de un campo. |
| `functions` |Opcional. Tenga en cuenta que una función de puntuación solo puede ser aplicada toofields filtrables. |
| `type` |Obligatorio para las funciones de puntuación. Indica el tipo de saludo de la función toouse. Entre los valores válidos se incluyen `magnitude`, `freshness`, `distance` y `tag`. Puede incluir más de una función en cada perfil de puntuación. nombre de la función Hello debe estar en minúsculas. |
| `boost` |Obligatorio para las funciones de puntuación. Número positivo usado como multiplicador para el resultado sin formato. No puede ser too1 igual. |
| `fieldName` |Obligatorio para las funciones de puntuación. Una función de puntuación solo puede ser aplicados toofields que forman parte de la colección de campos de hello del índice de Hola y que son filtrables. Además, cada tipo de función introduce restricciones adicionales (índice de actualización se usa con campos de fecha y hora, magnitud con número entero o campos dobles, distancia con campos de ubicación y etiqueta con cadena o campos de colección de cadenas). Solo puede especificar un campo único por cada definición de función. De ejemplo, toouse magnitud dos veces en Hola mismo perfil, necesitaría definiciones de tooinclude dos magnitud, uno para cada campo. |
| `interpolation` |Obligatorio para las funciones de puntuación. Define la pendiente de Hola para qué Hola aumento de puntuación crece desde el inicio de hello del final del intervalo de hello toohello del intervalo de Hola. Entre los valores válidos se incluyen `linear` (predeterminado), `constant`, `quadratic` y `logarithmic`. Consulte [Establecer interpolaciones](#bkmk_interpolation) para más información. |
| `magnitude` |función de puntuación de magnitud de Hello es clasificaciones tooalter utilizado según Hola intervalo de valores para un campo numérico. Algunos ejemplos de uso más común de Hola de esto son:<ul><li>Las clasificaciones por estrellas: Alter Hola puntuación en función de valor Hola campo "Clasificación por estrellas" de Hola. Cuando dos elementos son relevantes, elemento de hello con clasificación superior Hola se mostrará en primer lugar.</li><li>Margen: Cuando dos documentos son relevantes, un minorista puede tooboost documentos que tienen mayores márgenes en primer lugar.</li><li>Haga clic en recuentos: para las aplicaciones que realizan el seguimiento, haga clic a través de acciones tooproducts o páginas, puede usar elementos de tooboost de magnitud que tienden a tooget Hola mayor cantidad de tráfico.</li><li>Cantidad de descargas: para las aplicaciones que realizan el seguimiento de las descargas, Hola magnitud función permite aumentar elementos que tienen hello más descargados.</li></ul> |
| `magnitude:boostingRangeStart` |Hola conjuntos valor inicial del intervalo de hello en el cual se puntúa la magnitud. Hola valor debe ser un entero o un número de punto flotante. En cuanto a las clasificaciones por estrellas de 1 a 4, esto equivaldría a 1. Para los márgenes superiores al 50%, esto equivaldría a 50. |
| `magnitude:boostingRangeEnd` |Establece el valor de final de Hola de intervalo de hello en el cual se puntúa la magnitud. Hola valor debe ser un entero o un número de punto flotante. En cuanto a las clasificaciones por estrellas de 1 a 4, esto equivaldría a 4. |
| `magnitude:constantBoostBeyondRange` |Los valores válidos son true o false (valor predeterminado). Cuando se establece tootrue, aumento completo Hola continuará toodocuments tooapply que tienen un valor para el campo de destino de hello es mayor que el extremo superior de hello del intervalo de saludo. Si es false, aumento de Hola de esta función no será aplicado toodocuments tener un valor para el campo de destino de Hola que se encuentra fuera del intervalo de saludo. |
| `freshness` |función de puntuación de actualización de Hello es tooalter usado puntuaciones para los artículos basados en valores de DateTimeOffset campos de categoría. Por ejemplo, un elemento con una fecha más reciente puede clasificarse por encima de los elementos más antiguos. (Tenga en cuenta que también es posible toorank elementos como los eventos de calendario con fechas futuras que toohello más cerca de los elementos presente puede clasificarse por encima de elementos más Hola futuras). En la versión de servicio actual de hello, uno de los extremos del intervalo de Hola se corregirá toohello hora actual. Hello otro extremo es un tiempo en hello último en función de hello `boostingDuration`. tooboost un intervalo de horas en hello futuras usar negativo `boostingDuration`. tasa de Hello en qué Hola impulso cambios de un intervalo máximo y mínimo viene determinado por hello toohello de interpolación aplicar perfil de puntuación (Véase la figura hello). tooreverse Hola factor de aumento aplicado, elija un factor de aumento de menor que 1. |
| `freshness:boostingDuration` |Establece un período de caducidad después del que se detendrá la potenciación de un documento determinado. Vea [establecer boostingDuration](#bkmk_boostdur) Hola pasos de la sección de sintaxis y ejemplos. |
| `distance` |función de puntuación de distancia de Hello es hello tooaffect usado puntuación de documentos en función de cómo cerrar o ahora son ubicación geográfica de referencia de tooa relativa. ubicación de la referencia de Hola se proporciona como parte de la consulta de hello en un parámetro (mediante hello `scoringParameter` parámetro de consulta) como un argumento lon, LAT.. |
| `distance:referencePointParameter` |Un parámetro toobe pasa toouse consultas como ubicación de referencia. scoringParameter es un parámetro de consulta. Consulte [Búsqueda de documentos](search-api-2015-02-28-preview.md#SearchDocs) para obtener descripciones de los parámetros de consulta. |
| `distance:boostingDistance` |Número que indica la distancia de hello en kilómetros desde la ubicación de la referencia de Hola donde hello impulso intervalo finaliza. |
| `tag` |Hello etiqueta función de puntuación se utiliza puntuación de hello tooaffect de documentos basados en etiquetas en documentos y consultas de búsqueda. Se aumentar los documentos que tienen etiquetas en común con la consulta de búsqueda de Hola. Hola etiquetas para la consulta de búsqueda de Hola se proporciona como un parámetro de puntuación en cada solicitud de búsqueda (mediante hello `scoringParameter` parámetro de consulta). |
| `tag:tagsParameter` |Un parámetro toobe pasa en consultas toospecify etiquetas para una solicitud determinada. `scoringParameter` es un parámetro de consulta. Consulte [Búsqueda de documentos](search-api-2015-02-28-preview.md#SearchDocs) para obtener descripciones de los parámetros de consulta. |
| `functionAggregation` |Opcional. Se aplica solo cuando se especifican las funciones. Entre los valores válidos se incluyen `sum` (predeterminado), `average`, `minimum`, `maximum` y `firstMatching`. Una puntuación de búsqueda es un valor único que se calcula a partir de varias variables, incluidas varias funciones. Estos atributos se indica cómo se combinan los aumentos de Hola de todas las funciones de hello en un aumento agregado único que es aplicado toohello base puntuación del documento. puntuación de Hola se basa en hello tf idf valor calculado a partir de documentos de Hola y consulta de búsqueda de Hola. |
| `defaultScoringProfile` |Al ejecutar una solicitud de búsqueda, si no se especifica ningún perfil de puntuación, se usará la puntuación predeterminada (tf-idf solamente). Un nombre de perfil de puntuación predeterminado se puede establecer aquí, provocando toouse de búsqueda de Azure ese perfil cuando no se proporciona ningún perfil específico en la solicitud de búsqueda de Hola. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Establecer interpolaciones
Las interpolaciones le permiten pendiente de hello toodefine para qué Hola aumento de puntuación crece desde el inicio de hello del final del intervalo de hello toohello del intervalo de Hola. se puede utilizar Hola siguientes interpolaciones:

* `Linear`: Para los elementos que están dentro de hello max y min intervalo, Hola aumento aplicado toohello elemento se realizará en una cantidad constante decreciente. Lineal es interpolación de hello predeterminado para un perfil de puntuación.
* `Constant`: Para los elementos que están dentro de hello inicio y final del intervalo, un aumento constante será aplicado toohello resultados de rango.
* `Quadratic`: En la comparación tooa interpolación lineal que tiene un aumento constante decreciente, cuadrático inicialmente se reducirá a ritmo más pequeño y, a medida que se acerque el final del rango hello, se reducirá a intervalos mucho mayor. Esta opción de interpolación no se permite en funciones de puntuación de etiquetas.
* `Logarithmic`: En la comparación tooa interpolación lineal que tiene un aumento constante decreciente, logarítmica inicialmente se reducirá a ritmo más elevado y, a medida que se acerque el final del rango hello, se reducirá a intervalos mucho más pequeños. Esta opción de interpolación no se permite en funciones de puntuación de etiquetas.

<a name="Figure1"></a>![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Establecer boostingDuration
`boostingDuration`es un atributo de la función de actualización de hello. Se utiliza tooset un período de caducidad después de la cual el aumento se detendrá para un documento determinado. Por ejemplo, tooboost una línea de productos o marca durante un período de promoción de 10 días, especificaría el período de 10 días hello como "P10D" para dichos documentos. O tooboost próximos eventos Hola semana siguiente especifican "-P7D".

`boostingDuration` debe tener el formato de un valor "dayTimeDuration" XSD (subconjunto restringido de un valor de duración ISO 8601). patrón de Hola para esto es: `[-]P[nD][T[nH][nM][nS]]`.

Hello en la tabla siguiente proporciona varios ejemplos.

| Duration | boostingDuration |
| --- | --- |
| 1 día |"P1D" |
| 2 días, 12 horas |"P2DT12H" |
| 15 minutos |"PT15M" |
| 30 días, 5 horas, 10 minutos y 6,334 segundos |"P30DT5H10M6.334S" |

Para obtener más ejemplos, consulte [Esquema XML: tipos de datos (sitio web de W3.org)](http://www.w3.org/TR/xmlschema11-2/).

**Consulte también**
[API de REST del servicio Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) en MSDN <br/>
[Crear índice (API de Azure Search)](http://msdn.microsoft.com/library/azure/dn798941.aspx) en MSDN<br/>
[Agregar un índice de búsqueda de puntuación perfil tooa](http://msdn.microsoft.com/library/azure/dn798928.aspx) en MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
