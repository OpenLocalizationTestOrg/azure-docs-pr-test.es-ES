---
title: "resultados de búsqueda de toopage de aaaHow en búsqueda de Azure | Documentos de Microsoft"
description: "Paginación de Búsqueda de Azure, un servicio de búsqueda hospedado en la nube en Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Cómo resultados de búsqueda de toopage en búsqueda de Azure
Este artículo proporciona instrucciones sobre cómo toouse Hola API de REST de servicio de búsqueda de Azure tooimplement elementos estándar de una búsqueda de página de resultados, como los recuentos totales, la recuperación de documentos, criterios de ordenación y la navegación.

En cada caso mencionado a continuación, se especifican opciones relacionadas con la página que contribuyen a datos o información de la página de resultados de búsqueda tooyour a través de hello [Buscar documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) las solicitudes enviadas tooyour servicio de búsqueda de Azure. Las solicitudes incluyen un comando GET, ruta de acceso y parámetros de consulta que informan sobre lo que se solicita el servicio de Hola y cómo tooformulate Hola respuesta.

> [!NOTE]
> Una solicitud válida incluye una serie de elementos, como una dirección URL del servicio y la ruta de acceso, el verbo HTTP, `api-version`, etc. Para mayor brevedad, se recortan Hola ejemplos toohighlight Hola simplemente sintaxis toopagination relevante. Vea hello [API de REST de servicio de búsqueda de Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentación para obtener más información acerca de la sintaxis de la solicitud.
> 
> 

## <a name="total-hits-and-page-counts"></a>Total de resultados y recuentos de página
Mostrar hello total número de resultados devueltos por una consulta y, a continuación, devolverlos resultados en fragmentos más pequeños, es fundamental toovirtually todas las páginas de búsqueda.

![][1]

En la búsqueda de Azure, use hello `$count`, `$top`, y `$skip` parámetros tooreturn estos valores. Hello en el ejemplo siguiente se muestra una solicitud de ejemplo para el total de aciertos, formando `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Recuperar los documentos en los grupos de 15 y también muestran Hola total de aciertos, empezando por la primera página de hello:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Paginar resultados requiere `$top` y `$skip`, donde `$top` especifica el número de elementos de tooreturn en un lote, y `$skip` especifica el número de elementos de tooskip. Hola siguiente ejemplo, cada página muestra hello 15 a continuación de los elementos, indicado por saltos incremental de Hola Hola `$skip` parámetro.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Diseño
En una página de resultados de búsqueda, puede que desee tooshow una imagen en miniatura, un subconjunto de campos y una página de vínculo tooa producto completo.

 ![][2]

En búsqueda de Azure, usaría `$select` y una búsqueda de comandos tooimplement esta experiencia.

tooreturn un subconjunto de campos para un diseño en mosaico:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Imágenes y archivos multimedia no se puede buscar directamente y deberían almacenarse en otra plataforma de almacenamiento, como almacenamiento de blobs de Azure, los costos de tooreduce. En el índice de Hola y documentos, defina un campo que almacena la dirección URL de Hola de contenido externo de Hola. A continuación, puede usar el campo de hello como referencia de una imagen. imagen de toohello de Hello dirección URL debe estar en el documento de Hola.

tooretrieve página de descripción de un producto para un **onClick** evento, use [búsqueda de documento](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass en clave de Hola de hello documento tooretrieve. Hola de tipo de datos de clave de hello es `Edm.String`. En este ejemplo, es *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Ordenar por relevancia, clasificación o precio
Criterios de ordenación a menudo predeterminado toorelevance, pero es común toomake alternativos de ordenación estén disponibles para que los clientes pueden reorganizar rápidamente los resultados existentes en un orden diferente del rango.

 ![][3]

En búsqueda de Azure, la ordenación se basa en hello `$orderby` expresión para todos los campos que se indizan como`"Sortable": true.`

La relevancia está estrechamente asociada con perfiles de puntuación. Puede usar Hola de puntuación predeterminado, que basa en el orden de toorank de análisis y las estadísticas de texto todos los resultados, con las puntuaciones más altas sucediendo toodocuments más fuertes o más coincidencias con un término de búsqueda.

Criterios de ordenación alternativos se suelen estar asociados a **onClick** eventos que devuelva la llamada tooa método que genera el criterio de ordenación de Hola. Por ejemplo, con este elemento de página:

 ![][4]

Deberá crear un método que acepta la opción de ordenación de hello seleccionado como entrada y devuelve una lista ordenada de los criterios de hello asociados a esa opción.

 ![][5]

> [!NOTE]
> Mientras la puntuación de hello predeterminada es suficiente para muchos escenarios, se recomienda basar relevancia en un perfil de puntuación personalizado en su lugar. Un perfil de puntuación personalizado ofrece un elementos de tooboost de manera que son más beneficioso para el negocio tooyour. Consulte [Incorporación de un perfil de puntuación](http://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información. 
> 
> 

## <a name="faceted-navigation"></a>Navegación por facetas
Navegación de búsqueda es común en una página de resultados, normalmente situada al lado de Hola o la parte superior de una página. En Búsqueda de Azure, la navegación por facetas proporciona una búsqueda autodirigida basándose en filtros predefinidos. Consulte [Navegación por facetas en Búsqueda de Azure](search-faceted-navigation.md) para obtener más detalles

## <a name="filters-at-hello-page-level"></a>Filtros de nivel de página Hola
Si el diseño de la solución incluye páginas de búsqueda dedicado para determinados tipos de contenido (por ejemplo, una aplicación comercial en línea que tiene departamentos aparece al principio de Hola de página de hello), puede insertar una expresión de filtro junto con un **onClick** tooopen una página en un estado prefiltrada de eventos. 

Puede enviar un filtro con o sin expresión de búsqueda. Por ejemplo, hello solicitud siguiente se filtrará en nombre de la marca, devolver únicamente los documentos que coinciden con él.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Consulte [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) (Búsqueda de documentos [API de Azure Search]) para más información sobre las expresiones `$filter`.

## <a name="see-also"></a>Otras referencias
* [API de REST del Servicio Búsqueda de Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Operaciones de índice](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Operaciones del documento](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Vídeo y tutoriales acerca de Búsqueda de Azure](search-video-demo-tutorial-list.md)
* [Navegación por facetas en Búsqueda de Azure](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
