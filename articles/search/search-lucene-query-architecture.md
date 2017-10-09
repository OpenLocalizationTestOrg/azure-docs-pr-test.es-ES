---
title: "arquitectura de (Lucene) del motor de búsqueda de texto de aaaFull en búsqueda de Azure | Documentos de Microsoft"
description: "Explicación de conceptos de recuperación de procesamiento y documentos para la consulta de Lucene para la búsqueda de texto completo, como relacionado tooAzure búsqueda."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Cómo funciona la búsqueda de texto completo en Azure Search

Este artículo está dirigido a desarrolladores que necesitan un conocimiento más profundo sobre cómo funciona la búsqueda de texto completo de Lucene en Azure Search. Para las consultas de texto, Azure Search ofrecerá perfectamente resultados esperados en la mayoría de los escenarios, pero en ocasiones, podría obtener un resultado que parezca "desconectado" de algún modo. En estas situaciones, que tienen un fondo en Hola cuatro fases de ejecución de la consulta de Lucene (consultar análisis análisis léxico, búsqueda de coincidencias, la puntuación del documento) puede ayudar a identificar los cambios concretos tooquery parámetros o un índice de configuración que se entregará Hola resultado deseado. 

> [!Note] 
> Azure Search usa Lucene para la búsqueda de texto completo, pero la integración de Lucene no es exhaustiva. Se exponen selectivamente y ampliar Lucene funcionalidad tooenable Hola escenarios importante tooAzure búsqueda. 

## <a name="architecture-overview-and-diagram"></a>Introducción a la arquitectura y diagrama

Procesa una consulta de búsqueda de texto completo se inicia con términos de búsqueda de tooextract de texto de consulta de Hola de análisis. motor de búsqueda de Hello usa un tooretrieve indizar documentos con términos de búsqueda de coincidencias. Términos de consulta individuales a veces se desglosan y RECONSTITUYEN en nueva toocast de formularios a una red más amplia sobre lo que se podrían considerar como una posible coincidencia. Un conjunto de resultados, a continuación, se ordena por un relevancia puntuación asignado tooeach coincidentes documento individual. Los de la parte superior de Hola de hello lista el rango se devuelven toohello de aplicación que llama.

Una vez reformulada, la ejecución de la consulta tiene cuatro fases: 

1. Consulta de análisis 
2. Análisis léxico 
3. Recuperación de documentos 
4. Puntuación 

Hola diagrama siguiente muestra hello componentes utilizados tooprocess una solicitud de búsqueda. 

 ![Diagrama de la arquitectura de la consulta de Lucene en Azure Search][1]


| Componentes claves | Descripción funcional | 
|----------------|------------------------|
|**Analizadores de consulta** | Separar términos de consulta de operadores de consulta y crear el motor de búsqueda de toohello de toobe enviado Hola consulta estructura (árbol de consulta). |
|**Analizadores** | Realice un análisis léxico sobre los términos de consulta. Este proceso puede implicar la transformación, eliminación o expansión de los términos de consulta. |
|**Índice** | Una estructura de datos eficaz usar toostore y organizar puede buscar términos extraídos de los documentos indizados. |
|**Motor de búsqueda** | Recupera y las puntuaciones de coincidencia de documentos basadas en contenido de Hola de hello índice invierten. |

## <a name="anatomy-of-a-search-request"></a>Anatomía de una solicitud de búsqueda

Una solicitud de búsqueda es una especificación completa de lo que se debe devolver en un conjunto de resultados. En su forma más simple, es una consulta vacía sin ningún criterio de ningún tipo. Un ejemplo más realista incluye parámetros, varios términos, quizás con ámbito toocertain campos, con reglas de ordenación y posiblemente una expresión de filtro de consulta.  

el ejemplo siguiente se Hello es una solicitud de búsqueda podría enviar tooAzure búsqueda con hello [API de REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Para esta solicitud, el motor de búsqueda de Hola Hola después de:

1. Filtra los documentos cuyo precio de hello sea al menos 60 dólares y menos de 300 USD.
2. Ejecuta la consulta de Hola. En este ejemplo, consulta de búsqueda de hello consta de frases y términos: `"Spacious, air-condition* +\"Ocean view\""` (por lo general, los usuarios no accede signos de puntuación, pero incluido en el ejemplo de Hola nos permite tooexplain cómo analizadores controlen). Para esta consulta, el motor de búsqueda de Hola examina descripción Hola y campos de título especifican en `searchFields` para documentos que contengan "Vista marina" y además en términos de Hola "suficientes" o en términos que comienzan por el prefijo de Hola "air-condition". Hola `searchMode` parámetro es toomatch usado en cualquier término (valor predeterminado) o todos ellos, para los casos donde no se requiere de forma explícita un término (`+`).
3. Pedidos Hola conjunto resultante de hoteles por proximidad tooa geography ubicación dada y, a continuación, devuelve la aplicación que realiza la llamada toohello. 

Hola mayoría de este artículo es sobre el procesamiento de hello *consulta de búsqueda*: `"Spacious, air-condition* +\"Ocean view\""`. El filtrado y la ordenación están fuera del ámbito. Para obtener más información, vea hello [documentación de referencia de API de búsqueda](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Fase 1: Consulta de análisis 

Como se indicó, cadena de consulta de hello es Hola primera línea de solicitud de hello: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

Analizador separa los operadores de consulta de Hello (como `*` y `+` en el ejemplo de Hola) de búsqueda de términos y consulta de búsqueda de hello en se deconstruyen *subconsultas* de un tipo admitido: 

+ *consulta de término* para términos independiente (como "espacioso")
+ *consultas de frases* de términos entre comillas (como "vistas al mar")
+ *consulta de prefijo* de términos seguidos por un operador de prefijo `*` (como "post-vacacional")

Para obtener una lista completa de tipos de consultas admitidas, consulte [Sintaxis de consulta de Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Operadores asociados con una subconsulta determinan si consulta Hola "debe ser" o "debe ser" satisfecho en orden para un documento toobe considera una coincidencia. Por ejemplo, `+"Ocean view"` "deben" due toohello `+` operador. 

Analizador de consultas de Hello reestructura subconsultas hello en un *árbol de consulta* (una estructura interna que representa la consulta de Hola) pasa en el motor de búsqueda de toohello. Hola primera fase de consulta de análisis, árbol de consulta de hello presenta el siguiente aspecto.  

 ![Modo de búsqueda de consulta booleana][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Analizadores admitidos: versión simple y completa de Lucene 

 Azure Search expone dos lenguajes de consulta diferentes, `simple` (valor predeterminado) y `full`. Al establecer hello `queryType` parámetro con su solicitud de búsqueda, puede indicar analizador de consultas de Hola y lenguaje de consulta que se elija para que sepa cómo toointerpret Hola operadores y sintaxis. Hola [lenguaje de consulta Simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) es intuitivo y sólidos, proporcionados por el usuario toointerpret adecuado a menudo como: sin procesamiento del lado cliente. Admite los operadores de consulta familiares desde motores de búsqueda web. Hola [lenguaje de consulta completa Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), que obtendrá estableciendo `queryType=full`, amplía el idioma de consulta Simple de hello predeterminado mediante la adición de compatibilidad con varios operadores y tipos de consulta como carácter comodín, aproximada, regex y consultas centrada en el campo. Por ejemplo, una expresión regular enviada con la sintaxis de consulta simple se interpretaría como una cadena de consulta y no una expresión. solicitud de ejemplo de Hola en este artículo usa el lenguaje de consulta de hello Lucene completa.

### <a name="impact-of-searchmode-on-hello-parser"></a>Impacto de searchMode en Analizador de Hola 

Otro parámetro de solicitud de búsqueda que afecte a analizar es hello `searchMode` parámetro. Controla el operador predeterminado de Hola para consultas booleanas: cualquier valor (predeterminado) o todos.  

Cuando `searchMode=any`, que es el predeterminado de hello, delimitador de espacio de hello entre suficientes y air-condition es o (`||`), que realiza el texto de consulta de ejemplo de Hola equivalente a: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Operadores explícitos, como `+` en `+"Ocean view"`, no son ambiguos en construcción de consulta booleana (término de hello *debe* coincidan con). Es menos obvio cómo términos hello toointerpret restante: suficientes y air-condition. ¿Motor de búsqueda de hello debería encontrar coincidencias en la vista al mar *y* suficientes *y* air-condition? ¿O bien debe encontrar a la vista al mar más *ninguna de ellas* de hello restantes términos? 

De forma predeterminada (`searchMode=any`), motor de búsqueda de hello supone interpretación más amplia de Hola. El campo *debe* coincidir, reflejar la semántica "o". árbol de consulta inicial de Hola muestra anteriormente, con hello dos operaciones de "debería", se muestra hello predeterminado.  

Imagine que establecemos ahora `searchMode=all`. En este caso, el espacio de Hola se interpreta como una operación "y". Cada uno de los términos de hello restantes debe estar presente en hello documento tooqualify como una coincidencia. consulta de ejemplo de Hola resultante podría interpretarse del siguiente modo: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Un árbol de consulta modificada para esta consulta sería como sigue, donde un documento coincidente es la intersección de Hola de todas las tres subconsultas: 

 ![Consulta booleana searchmode all][3]

> [!Note] 
> Elegir `searchMode=any` sobre `searchMode=all` es la mejor decisión cuando se ejecutan consultas representativas. Los usuarios que son operadores de tooinclude probable (común cuando se almacena el documento de búsqueda) que encuentre resultados más intuitiva si `searchMode=all` informa construcciones de consulta booleana. Para obtener más información acerca de la interacción de hello entre `searchMode` y operadores, vea [sintaxis de consulta Simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Fase 2: Análisis léxico 

Proceso de analizadores léxico *término consultas* y *frase consultas* después de la estructura de árbol de la consulta de Hola. Un analizador acepta Hola texto entradas dado tooit analizador hello, procesos Hola texto y, a continuación, términos envía volver acortado incorporar toobe Hola árbol de la consulta. 

Hola de forma más habitual de análisis léxico es *análisis lingüístico* que transforma los términos de consulta basados en reglas tooa específico dado idioma: 

* Reducir un formulario de consulta término toohello raíz de una palabra 
* Eliminación de palabras no esenciales (palabras irrelevantes, como "el" o "y") 
* División de una palabra compuesta en partes 
* Uso de minúsculas en una palabra con mayúsculas 

Todas estas operaciones suelen tooerase diferencias entre las entradas de texto hello proporcionada por los términos de hello y usuario Hola almacenados en el índice de Hola. Tales operaciones ir más allá de procesamiento de texto y requieren un conocimiento profundo del lenguaje de hello propio. tooadd este nivel de reconocimiento lingüístico, búsqueda de Azure es compatible con una lista larga de [analizadores de lenguaje](https://docs.microsoft.com/rest/api/searchservice/language-support) de Lucene y Microsoft.

> [!Note]
> Los requisitos de análisis pueden oscilar entre tooelaborate mínimo según el escenario. Puede controlar la complejidad de análisis léxico Hola seleccionando uno de los analizadores de hello predefinido o creando su propio [analizador personalizado](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Analizadores son campos toosearchable ámbito y se especifican como parte de una definición de campo. Esto le permite análisis léxico toovary por campo. No se especifica, Hola *estándar* se utiliza el analizador de Lucene.

En nuestro ejemplo, tooanalysis anterior, árbol de consulta inicial de hello tiene término Hola "Spacious" con una "S" mayúscula y una coma que Hola analizador de consultas interpreta como parte del término de la consulta de hello (una coma no se considera un operador de lenguaje de consulta).  

Cuando analizador de hello predeterminado procesa término hello, minúsculas "vista al mar" y "suficientes" y quite el carácter de coma Hola. árbol de la consulta modificada de Hello será como se indica a continuación: 

 ![Consulta booleana con términos analizados][4]

### <a name="testing-analyzer-behaviors"></a>Prueba de comportamientos del analizador 

comportamiento de Hola de un analizador se puede probar mediante hello [API analizar](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Proporcionar texto hello que desea tooanalyze toosee qué términos dados analizador generará. Por ejemplo, toosee cómo procesaría analizador estándar Hola Hola texto "air-condition", puede emitir Hola después de solicitud:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

Analizador estándar Hola divide el texto de entrada de hello en hello siguiendo dos tokens, anotarlos con atributos como inicio y desplazamientos de extremo (utilizados para resultados destacados), así como su posición (que se usa para la coincidencia de frase):

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Análisis de toolexical de excepciones 

Análisis léxico aplica solo los tipos de tooquery que necesitan obtener todos los términos: consulta de un término o una consulta de la frase. No se aplica tipos tooquery incompleta términos: consulta de prefijo, consultas de carácter comodín, consulta de expresión regular: o tooa aproximada consulta. Los tipos, incluidos la consulta de prefijo de hello con el término de consulta *air-condition\**  en nuestro ejemplo, se agregan directamente toohello árbol de consulta, omitiendo la fase de análisis de Hola. Hello solo se realiza en términos de consulta de los tipos de transformación es escribir.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Fase 3: Recuperación de documentos 

Recuperación de documentos refiere toofinding documentos con los términos de búsqueda de coincidencias de índice Hola. Esta fase se entiende mejor mediante un ejemplo. Puede empezar con un índice de hoteles tener Hola después de esquema simple: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Suponga también que este índice contiene Hola después de cuatro documentos: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Cómo se indexan los términos**

recuperación de toounderstand, le ayuda a tooknow algunos conceptos básicos acerca de la indización. unidad de Hola de almacenamiento es un índice invertido, uno para cada campo de búsqueda. Dentro de un índice invertido hay una lista ordenada de todos los términos de todos los documentos. Cada término asigna toohello lista de documentos en el que aparece, como evidentes en el siguiente ejemplo de Hola.

términos de hello tooproduce en un índice invertido, motor de búsqueda de hello realiza análisis léxico sobre el contenido de Hola de documentos, toowhat similar se produce durante el procesamiento de consultas. Entradas de texto se pasan tooan analizador, en minúsculas, que se han quitado de puntuación y así sucesivamente, dependiendo de la configuración de analizador de Hola. Es común, aunque no necesario, toouse Hola mismo analizadores de búsqueda y las operaciones de indización para que los términos de consulta parecen más a los términos de un índice de Hola.

> [!Note]
> Azure Search le permite especificar diferentes analizadores para la indexación y búsqueda a través de parámetros de campo `indexAnalyzer` y `searchAnalyzer` adicionales. Si no se especifica, Hola analizador establecido con hello `analyzer` propiedad se utiliza para la indización y búsqueda.  

**Índice invertido para documentos de ejemplo**

Devolver tooour por ejemplo, en hello **título** campo, índice invertido de hello el siguiente aspecto:

| Término | Lista de documento |
|------|---------------|
| atman | 1 |
| playa | 2 |
| hotel | 1, 3 |
| océano | 4  |
| playa | 3 |
| resort | 3 |
| retirada | 4 |

En el campo de título de hello, solo *hotel* aparece en dos documentos: 1, 3.

Para hello **descripción** campo, índice hello es como sigue:

| Término | Lista de documento |
|------|---------------|
| post- | 3
| y | 4
| playa | 1
| vacacional | 3
| cómodo | 3
| distancia | 1
| isla | 2
| kauaʻi | 2
| ubicado | 2
| norte | 2
| océano | 1, 2, 3
| de | 2
| en |2
| silencioso | 4
| habitaciones  | 1, 3
| aislado | 4
| costa | 2
| espacioso | 1
| Hola | 1, 2
| demasiado| 1
| view | 1, 2, 3
| paseo | 1
| por | 3


**Coincidencia de términos de consulta con términos indexados**

Vamos a dada índices Hola invertido anteriores, devolver la consulta de ejemplo de toohello y vea cómo coincidentes documentos se encuentran para nuestra consulta de ejemplo. Recuerde que ese árbol de consulta final hello tiene el siguiente aspecto: 

 ![Consulta booleana con términos analizados][4]

Durante la ejecución de la consulta, las consultas individuales se ejecutan en los campos de búsqueda de Hola por separado. 

+ Hello TermQuery "suficientes", coincide con documento 1 (Hotel Atman). 

+ Hola PrefixQuery, "air-condition *", no coincide con todos los documentos. 

  Este es el comportamiento que normalmente confunde a los desarrolladores. Aunque el término Hola con aire acondicionado existe en el documento de hello, se divide en dos términos analizador de Hola de forma predeterminada. Recuerde que las consultas de prefijo, que contienen términos parciales, no se analizan. Por lo tanto, términos con el prefijo "air-condition" se busca en hello índice invierten y no se encuentran.

+ Hello PhraseQuery "vista marina", busca Hola términos "océano" y "vista" y comprueba la proximidad de Hola de términos en el documento original de Hola. Documentos de 1, 2 y 3 coincide con esta consulta en el campo de descripción de Hola. Documento de aviso 4 tiene Océano de término de hello en el título de hello pero no se considera a una coincidencia, buscamos frase de "vista al mar" Hola, en lugar de las palabras individuales. 

> [!Note]
> Una consulta de búsqueda se ejecuta de forma independiente en todos los campos que permiten búsqueda Hola índice de búsqueda de Azure, a menos que limite los campos de hello establecido con hello `searchFields` parámetro, como se muestra en la solicitud de búsqueda de ejemplo de Hola. Se devuelven documentos que coinciden en cualquiera de los campos de hello seleccionado. 

En hello todo para consulta de hello en cuestión, documentos de Hola que coinciden con son 1, 2, 3. 

## <a name="stage-4-scoring"></a>Fase 4: Puntuación  

A todos los documentos de un conjunto de resultados de búsqueda se les asigna una puntuación de relevancia. función Hello de puntuación por relevancia hello es toorank superior de los documentos que la mejor respuesta para un usuario pregunta expresados por la consulta de búsqueda de Hola. Hola puntuación se calcula en función de propiedades estadísticas de términos que coinciden. En hello núcleo de hello puntuación fórmula es [TF/IDF (frecuencia de frecuencia inversa de documento de término)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). En las consultas que contienen términos comunes y poco frecuentes, TF/IDF promueve resultados que contengan el término raras Hola. Por ejemplo, en un índice hipotético con todos los artículos de Wikipedia, desde documentos esa consulta coincidente hello *president hello*, documentos de búsqueda de coincidencias *president* se consideran más importantes que documentos de búsqueda de coincidencias *la*.


### <a name="scoring-example"></a>Ejemplo de puntuación

Recuerde Hola tres documentos que coinciden con la consulta de ejemplo:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

Documento 1 consulta coincidente Hola mejor porque ambos Hola término *suficientes* y una frase necesario hello *vista al mar* se producen en el campo de descripción de Hola. documentos de dos de Hello coinciden con la frase de hello solo *vista al mar*. Podría ser sorprendente ese puntuación por relevancia Hola de documento 2 y 3 es diferente, aunque se comparar consultas Hola Hola igual. Es porque Hola puntuación fórmula tiene componentes más que simplemente TF/IDF. En este caso, al documento 3 se le asignó una puntuación ligeramente superior porque su descripción es más corta. Obtenga información acerca de [práctico puntuación fórmula Lucene](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand la longitud de campo y otros factores pueden influir en Hola puntuación por relevancia.

Algunos tipos (comodín, el prefijo y regex) de consulta siempre aporta una puntuación constante toohello general de puntuación de documentos. Esto permite que las coincidencias encontradas a través de toobe de expansión de consulta incluido en los resultados de hello, pero sin afectar a la clasificación de Hola. 

El ejemplo muestra por qué esto es importante. Búsquedas con caracteres comodín, incluidas las búsquedas de prefijo, son ambiguas por definición dado Hola entrada es una cadena parcial con coincidencias posibles en un gran número de términos dispares (tenga en cuenta una entrada de "paseo *", con las coincidencias encontradas en "tours", "tourettes", y " tourmaline"). Dada la naturaleza de Hola de estos resultados, no hay ninguna manera tooreasonably deducir cuáles son los términos son más valiosos que otros usuarios. Por este motivo, se omiten las frecuencias de término cuando realiza la puntuación de resultados en consultas de tipo caracteres comodín, prefijo y regex. En una solicitud de búsqueda de varias partes que incluye términos parciales y totales, se incorporan los resultados a partir de datos parcial Hola con una constante puntuación tooavoid sesgo hacia coincidencias potencialmente inesperadas.

### <a name="score-tuning"></a>Optimización de la puntuación

Hay dos maneras de puntuaciones de importancia tootune en búsqueda de Azure:

1. **Los perfiles de puntuación** promover documentos en la lista de hello el rango de resultados en función de un conjunto de reglas. En nuestro ejemplo, podríamos consideramos documentos que coinciden en el campo de título de hello más importantes que documentos que se encuentran coincidencias en el campo de descripción de Hola. Además, si el índice tenía un campo de precio para cada hotel, podríamos favorecer a los documentos con un precio menor. Obtener más información cómo demasiado[agregar índice de búsqueda de tooa de perfiles de puntuación.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Aumento de términos** (disponible solo en la sintaxis de consulta de Lucene completa de hello) proporciona un operador de aumento `^` que se puede aplicar tooany parte del árbol de la consulta de Hola. En nuestro ejemplo, en lugar de Buscar prefijo hello *air-condition*\*, uno podría buscar cualquiera de los términos exactos hello *air-condition* o prefijo de hello, pero los documentos que coinciden en hello exacta término con un rango superior mediante la aplicación de consulta de aumento toohello término: *aire condición ^ 2 || AIR-Condition**. Más información sobre la [priorización de términos](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Puntuación en un índice distribuido

Todos los índices de búsqueda de Azure son automáticamente dividir en varias particiones, lo que nos tooquickly distribuir índice Hola entre varios nodos durante la escala del servicio de una copia de seguridad o reducir verticalmente. Cuando se emite una solicitud de búsqueda, se emite de forma independiente en cada partición. Hello resultados de cada partición se, a continuación, combinan y se ordenan por puntuación (si no se ha definido ninguna otra ordenación). Es importante tooknow que Hola puntuación función pesos término frecuencia de las consultas con su frecuencia de documento inverso en todos los documentos dentro de la partición hello, no a través de todas las particiones.

Esto significa que una puntuación por relevancia *puede* ser diferente para los documentos idénticos si residen en diferentes particiones. Afortunadamente, tales diferencias suelen toodisappear a medida que aumenta el número de Hola de documentos en el índice de hello debido distribución de término incluso toomore. No es posible tooassume en qué partición se colocará cualquier documento concreto. Sin embargo, suponiendo que no cambia una clave de documento, siempre se asignará toohello misma partición.

En general, puntuación de documento no es atributo mejor de Hola para ordenar los documentos si la estabilidad de orden es importante. Por ejemplo, proporciona dos documento con una puntuación idéntica, no hay ninguna garantía de que aparece en primer lugar en las ejecuciones posteriores de Hola misma consulta. Puntuación del documento sólo debe dar una idea general de relevancia de documento relativa tooother documentos en conjunto de resultados de Hola.

## <a name="conclusion"></a>Conclusión

éxito de Hola de motores de búsqueda de internet ha generado expectativas para la búsqueda de texto completo sobre datos privados. Para casi cualquier tipo de experiencia de búsqueda, ahora esperamos Hola motor toounderstand nuestra intención, incluso cuando términos son incorrectas o está incompleto. Esperamos incluso coincidencias basadas en términos casi equivalentes o sinónimos que realmente nunca hemos especificado.

Desde un punto de vista técnico, búsqueda de texto completo es muy compleja, que requieren el análisis lingüístico sofisticado y un enfoque sistemático tooprocessing de maneras que refinar, expandan y para transforman toodeliver de términos de consulta resultado correspondiente. Dado las complejidades inherentes de hello, hay muchos factores que pueden afectar al resultado de hello de una consulta. Por esta razón, invertir la mecánica de hello tiempo toounderstand Hola de búsqueda de texto completo ofrece ventajas tangibles al tratar de toowork a través de resultados inesperados.  

En este artículo se han explorado búsqueda de texto completo en el contexto de Hola de búsqueda de Azure. Esperamos que proporciona suficientes fondo toorecognize posibles causas y soluciones para resolver problemas comunes de las consultas. 

## <a name="next-steps"></a>Pasos siguientes

+ Generar índice de ejemplo de Hola, pruebe distintas consultas y revisar los resultados. Para obtener instrucciones, consulte [crear y consultar un índice en el portal de hello](search-get-started-portal.md#query-index).

+ Pruebe la sintaxis de consulta adicional de hello [buscar documentos](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) sección ejemplo o de [sintaxis de consulta Simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) en el Explorador de búsqueda en el portal de Hola.

+ Revisión [perfiles de puntuación](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) si desea tootune clasificar de la aplicación de búsqueda.

+ Obtenga información acerca de cómo tooapply [analizadores léxicos específica del lenguaje](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Configurar los analizadores personalizados](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) para un procesamiento mínimo o especializado en campos específicos.

+ [Comparar el analizador estándar y el analizador de inglés](http://alice.unearth.ai/) en paralelo en este sitio web de demostración. 

## <a name="see-also"></a>Otras referencias

[API de REST de documentos de búsqueda](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Sintaxis de consulta simplificada](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Sintaxis de consulta completa de Lucene ](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Control de los resultados de la búsqueda](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
