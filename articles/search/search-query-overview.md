---
title: "Índice de la búsqueda de Azure aaaQuery | Documentos de Microsoft"
description: "Crear una consulta de búsqueda en búsqueda de Azure y usar resultados de búsqueda de toofilter y de ordenación de los parámetros de búsqueda."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Consultas en el índice de Búsqueda de Azure
> [!div class="op_single_selector"]
> * [Información general](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Al enviar las solicitudes de búsqueda tooAzure búsqueda, hay un número de parámetros que se pueden especificar junto con palabras reales Hola que se escriben en el cuadro de búsqueda de saludo de la aplicación. Estos parámetros de consulta permiten tooachieve cierto control más profunda de hello [experiencia de búsqueda de texto completo](search-lucene-query-architecture.md).

A continuación se muestra una lista que se explica brevemente los usos más comunes de parámetros de consulta de hello en búsqueda de Azure. Para obtener información detallada de parámetros de consulta y su comportamiento, vea Hola detallada páginas para hello [API de REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) y [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Tipos de consultas
Búsqueda de Azure ofrece muchas opciones toocreate muy eficaz las consultas. Hola dos tipos principales de consulta que se va a utilizar son `search` y `filter`. A `search` consulta busca de uno o varios términos en todos los *búsqueda* campos en el índice y funciona de manera Hola se podría esperar un motor de búsqueda como Google o Bing toowork. Una consulta `filter` evalúa una expresión booleana en todos los campos *filtrables* de un índice. A diferencia de `search` consultas, `filter` consultas coincide con contenido exacto de Hola de un campo, lo que significa que distinguen mayúsculas de minúsculas para los campos de cadena.

Puede usar los filtros y las búsquedas conjuntamente o por separado. Si utiliza conjuntamente, filtro de hello es aplicar primera toohello todo índice y, a continuación, en que se realiza la búsqueda de hello en los resultados de Hola de filtro de Hola. Filtros, por tanto, pueden ser un rendimiento de las consultas tooimprove técnica útil porque reducen conjunto Hola de documentos que Hola tooprocess de necesidades de consulta de búsqueda.

sintaxis de Hola para expresiones de filtro es un subconjunto de hello [idioma de filtro de OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Para las consultas de búsqueda puede usar cualquier hello [una sintaxis simplificada](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) o hello [sintaxis de consulta de Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) que se describen a continuación.

### <a name="simple-query-syntax"></a>Sintaxis de consulta simplificada
Hola [sintaxis de consulta simple](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) es lenguaje de consulta de hello predeterminado utilizado en la búsqueda de Azure. sintaxis de consulta simple Hello es compatible con un número de operadores de búsqueda comunes incluidos hello AND, OR, NOT, frase, sufijo y operadores de precedencia.

### <a name="lucene-query-syntax"></a>sintaxis de consulta de Lucene
Hola [sintaxis de consulta de Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) permite hello toouse adoptado ampliamente y lenguaje de consulta más expresivo desarrollada como parte de [Lucene de Apache](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Con esta sintaxis de consulta permite tooeasily lograr Hola siguientes capacidades: [consultas centrada en el campo](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [búsqueda aproximada](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [búsqueda por proximidad](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ aumento de términos](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [búsqueda de expresión regular](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [búsqueda con caracteres comodín](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [aspectos básicos de la sintaxis](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), y [las consultas que utilizan operadores booleanos](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Ordenación de los resultados
Al recibir los resultados de una consulta de búsqueda, puede solicitar que la búsqueda de Azure sirve resultados Hola ordenadas según los valores de un campo determinado. De forma predeterminada, búsqueda de Azure ordena los resultados de la búsqueda de hello en función de clasificación de Hola de puntuación de búsqueda de cada documento, que se deriva de [TF IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Si desea que los resultados se ordenan por un valor distinto de puntuación de búsqueda de Hola de tooreturn de búsqueda de Azure, puede usar hello `orderby` parámetro de búsqueda. Puede especificar el valor de Hola de hello `orderby` campo de parámetro tooinclude nombres y llama a toohello [ `geo.distance()` función](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) para valores geoespaciales. Cada expresión puede ir seguida de `asc` tooindicate que se solicitan los resultados en orden ascendente, y `desc` tooindicate que se solicitan los resultados en orden descendente. clasificación predeterminada de Hello orden ascendente.

## <a name="paging"></a>Paginación
Búsqueda de Azure hace fácil tooimplement paginación de resultados de la búsqueda. Mediante el uso de hello `top` y `skip` parámetros, sin problemas, puede emitir las solicitudes de búsqueda que permitan que el conjunto total de hello tooreceive de resultados de búsqueda de subconjuntos administrables y ordenados que habilitar fácilmente las prácticas de interfaz de usuario de búsqueda eficaces. Cuando se reciben estos subconjuntos más pequeños de resultados, también puede recibir número Hola de documentos en conjunto total de Hola de resultados de la búsqueda.

Puede aprender más acerca de la paginación de resultados de la búsqueda en el artículo hello [cómo resultados de búsqueda de toopage en búsqueda de Azure](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Resaltado de referencias
En búsqueda de Azure, enfatizar parte exacta de Hola de resultados de la búsqueda que coincidan con la consulta de búsqueda de Hola se facilita mediante el uso de hello `highlight`, `highlightPreTag`, y `highlightPostTag` parámetros. Puede especificar qué *búsqueda* los campos deben tener el texto coincidente destacan, así como especificar devuelve Hola exacta cadena etiquetas tooappend toohello inicial y final de hello coincidencia del texto que la búsqueda de Azure.

## <a name="try-out-query-syntax"></a>Prueba de la sintaxis de consulta

diferencias de sintaxis de manera mejor de Hello toounderstand está enviando consultas y revisar los resultados.

+ Use [buscar en el explorador](search-explorer.md) Hola portal de Azure. Mediante la implementación de [índice de ejemplo de Hola](search-get-started-portal.md), puede consultar el índice de hello en minutos con las herramientas en el portal de Hola.

+ Use [Fiddler](search-fiddler.md) o Chrome Postman toosubmit consultas tooan índice que se ha cargado el servicio de búsqueda de tooyour. Ambas herramientas admiten el punto de conexión REST llamadas tooan HTTP. 
