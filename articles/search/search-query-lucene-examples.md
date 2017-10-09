---
title: "ejemplos de consultas de aaaLucene para la búsqueda de Azure | Documentos de Microsoft"
description: "Sintaxis de consulta de Lucene para la búsqueda aproximada, la búsqueda de proximidad, la priorización de términos, la búsqueda de expresiones regulares y la búsqueda con caracteres comodín"
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Ejemplos de sintaxis de consulta de Lucene para la creación de consultas en Búsqueda de Azure
Al construir consultas de búsqueda de Azure, puede usar cualquier predeterminado de hello [sintaxis de consulta simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) o una alternativa de hello [Lucene analizador de consultas de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Hola analizador de consultas de Lucene admite construcciones de consulta más complejas, como las consultas de ámbito de campo, búsqueda aproximada, búsqueda de proximidad, lo que incrementa el término y búsqueda de expresión regular.

En este artículo, puede ir a través de ejemplos de operaciones de consulta disponibles al utilizar la sintaxis completa de Hola.

## <a name="viewing-hello-examples-in-jsfiddle"></a>Ver ejemplos de hello en JSFiddle

Todos los ejemplos de hello en este artículo son consultas ejecutables que se ejecutan en un índice de búsqueda cargado previamente en [JSFiddle](https://jsfiddle.net), un editor de código en línea para probar la secuencia de comandos y HTML. 

toorun, haga doble clic en tooopen de direcciones URL de ejemplo Hola consulta JSFiddle en otra ventana del explorador.

> [!NOTE]
> en los ejemplos siguientes Hello aprovechan un índice de búsqueda que se compone de trabajos disponibles en función de un conjunto de datos proporcionada por hello [ciudad de Nueva York OpenData](https://nycopendata.socrata.com/) iniciativa. Estos datos no deben considerarse actuales o completos. índice de Hello está activado el servicio de espacio aislado suministrado por Microsoft. No necesita una suscripción de Azure o la búsqueda de Azure tootry estas consultas.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>¿Cómo tooinvoke completa de análisis de Lucene

Todos los ejemplos de hello en este artículo especifican hello **queryType = completa** parámetro, que indica que sintaxis completa de hello, controlada hello Lucene analizador de consultas de búsqueda. 

**Ejemplo 1** : Hola contextual después tooopen de fragmento de código de consulta en una nueva ventana del explorador de página que carga JSFiddle y se ejecuta Hola consulta:

* [&amp;queryType=full&amp;search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

En la nueva ventana del explorador hello, origen de JavaScript de Hola y de salida HTML se presentan en paralelo. script de Hola hace referencia a una consulta completa (hello no solo fragmento de código, tal y como se muestra en el vínculo de hello). consulta completa Hola se muestra en las direcciones URL de Hola para cada ejemplo. 

Esta consulta devuelve los documentos de nuestro índice de trabajos de la ciudad de Nueva York (nycjobs, cargados en un servicio de espacio aislado). Para mayor brevedad, consulta Hola especifica se devuelven solo los títulos de empresa. consulta completa Hello es como sigue:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Hola **searchFields** parámetro restringe el campo de título de negocio de hello búsqueda toojust Hola. Hola **queryType** se establece demasiado**completa**, que indica toouse hello Lucene analizador de consultas de búsqueda de Azure para esta consulta.

> [!NOTE]
> Para obtener información preliminar sobre el procesamiento de consultas, vea [Cómo funciona la búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md). Para más información sobre los parámetros de búsqueda, consulte [Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) [Búsqueda de documentos (API de REST del servicio Azure Search)].
>

### <a name="fielded-query-operation"></a>Operación de consulta clasificada por campos
Puede modificar los ejemplos de hello en este artículo especificando un **fieldname:searchterm** toodefine construcción una operación de consulta clasificadas por campos, donde el campo de hello es una sola palabra, y término de búsqueda de hello también es una sola palabra o frase, Opcionalmente, con operadores booleanos. Algunos ejemplos son los siguientes hello:

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

Ser seguro tooput varias cadenas entre comillas si desea que ambos toobe de cadenas que se evalúa como una sola entidad, como en este caso buscando dos ciudades distintas en el campo de ubicación de Hola. Además, asegúrese de operador de Hola se convierte en mayúsculas como se ve con NOT y and.

campo de Hello especificado en **fieldname:searchterm** debe ser un campo de búsqueda. Consulte [Creación de un índice (API de REST del servicio Azure Search)](https://docs.microsoft.com/rest/api/searchservice/create-index) para más información sobre cómo se usan los atributos de índice en las definiciones de campo.

**Ejemplo 2** : consulta de menú contextual Hola siguiente fragmento de esta consulta busca los títulos de empresa con hello término senior en ellos, pero no junior:

* [&amp;queryType=full&amp;search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Ejemplo de búsqueda aproximada
Una búsqueda aproximada busca coincidencias en términos que tienen una construcción similar. Según la [documentación de Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), las búsquedas aproximadas se basan en la [distancia Levenshtein-Damerau](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo una búsqueda aproximada, anexar tilde Hola "~" símbolos final Hola de una sola palabra con un parámetro opcional, un valor entre 0 y 2, que especifica la distancia de edición de Hola. Por ejemplo, "blue~" o "blue~1" devolvería blue, blues y glue.

**Ejemplo 3** --contextual Hola siguiente consulta se fragmento de código. Esta consulta busca los trabajos con la asociación de término hello (donde se está mal escrito):

* [&amp;queryType=full&amp;search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Las consultas aproximadas no se [analizan](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), lo cual puede resultar sorprendente si espera lematización. Solo se realizan análisis léxicos en términos completos (consulta de término o de expresión). Tipos de consulta con los términos incompletos (consulta de prefijo, consultas de carácter comodín, consulta de expresión regular, consulta aproximada) se agregan directamente toohello árbol de consulta, omitiendo la fase de análisis de Hola. Hello solo se realiza en términos de consulta incompleta transformación es escribir.
>

## <a name="proximity-search-example"></a>Ejemplo de búsqueda por proximidad
Búsquedas de proximidad son los términos de uso toofind que están cerca entre sí en un documento. Insertar una tilde "~" símbolo en hello final de una frase seguido por número de Hola de palabras que crear límites de proximidad de Hola. Por ejemplo, "aeropuerto hotel" ~ 5 encontrarán hotel de términos de Hola y aeropuerto dentro de 5 palabras entre sí en un documento.

**Ejemplo 4** : consulta de hello del menú contextual. Buscar trabajos con el término de Hola "analista" donde se es separar con no más de una palabra:

* [&amp;queryType=full&amp;search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Ejemplo 5** --Pruébelo nuevo quitar palabras hello entre término Hola "analista".

* [&amp;queryType=full&amp;search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Ejemplos de priorización de términos
Lo que incrementa el término hace referencia tooranking un documento más alto si contiene Hola impulsado término, toodocuments relativa que no contengan el término de Hola. Esto difiere de los perfiles de puntuación en los que aumentan ciertos campos, en lugar de términos específicos. Hello en el ejemplo siguiente se le ayuda a mostrar hello diferencias.

Considere la posibilidad de un perfil de puntuación que aumenta la devuelve en un campo determinado, como **género** en el ejemplo de Hola a musicstoreindex. Lo que incrementa el término podría ser utilizado toofurther aumento algunos de los términos de búsqueda más que otras. Por ejemplo, "rock ^ 2 electrónica" se aumentar los documentos que contengan los términos de búsqueda de Hola Hola **género** campo superior a otros campos que permiten búsqueda en índice Hola. Además, los documentos que contienen el término de búsqueda de Hola "rock" se clasificará superior Hola otro término de búsqueda "electronic" como resultado del valor de aumento de término de hello (2).

tooboost un término, símbolo de intercalación de uso hello, "^", símbolo con un factor de aumento (un número) al final de hello del término Hola está buscando. Hola mayor factor de aumento de hello, hello término de hello más relevante será relativa tooother términos de búsqueda. De forma predeterminada, el factor de aumento de hello es 1. Aunque el factor de aumento de hello debe ser positivo, puede ser menor que 1 (por ejemplo, 0,2).

**Ejemplo 6** : consulta de hello del menú contextual. Buscar trabajos con el término de Hola "analista de equipo", donde veremos no genera resultados con el equipo de palabras y analista, aunque las trabajos analista estén en parte superior de Hola de resultados de Hola.

* [&amp;queryType=full&amp;search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Ejemplo 7** --inténtelo de nuevo, este aumento del tiempo resultados con el equipo de término de Hola sobre analista de término de Hola si ambas palabras no existe.

* [&amp;queryType=full&amp;search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Ejemplo de expresión regular
Una búsqueda de expresión regular encuentra una coincidencia basada en contenido de hello entre barras diagonales "/", como Hola documentado en [clase RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Ejemplo 8** : consulta de hello del menú contextual. Buscar trabajos con el término de hello sénior o Junior.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

dirección URL de Hello en este ejemplo no se representará correctamente en la página de Hola. Como alternativa, copie Hola dirección URL siguiente y péguelo en la dirección URL del explorador Hola:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Ejemplo de búsqueda con caracteres comodín
Puede usar la sintaxis generalmente reconocida para búsquedas con caracteres comodín únicas (?) o múltiples (\*). Tenga en cuenta consulta de Lucene Hola analizador admite el uso de Hola de estos símbolos con un único término y no una frase.

**Ejemplo 9** : consulta de hello del menú contextual. Buscar los trabajos que contengan Hola prefijo 'programa' que incluiría títulos de empresa con términos de Hola de programación y programador en ella.

* [&amp;queryType=full&amp;$select=business_title&amp;search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

¿No puede utilizar un símbolo * o ? símbolo como primer carácter de una búsqueda de Hola.

## <a name="next-steps"></a>Pasos siguientes
Pruebe a especificar hello Lucene analizador de consultas en el código. Hola siguientes vínculos explica cómo tooset la búsqueda de las consultas para .NET y Hola API de REST. vínculos de Hello utilizar sintaxis simple de hello predeterminada por lo que deberá tooapply lo que aprendió de esta Hola de artículo toospecify **queryType**.

* [Consultar el índice de búsqueda de Azure con hello SDK para .NET](search-query-dotnet.md)
* [Consultar el índice de búsqueda de Azure con hello API de REST](search-query-rest-api.md)

## <a name="see-also"></a>Otras referencias

 [Cómo funciona la búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md)