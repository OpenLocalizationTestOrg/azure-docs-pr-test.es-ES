---
title: "aaaFrequently preguntas más frecuentes (P+F) sobre la búsqueda de Azure | Documentos de Microsoft"
description: "Obtenga respuestas toocommon preguntas acerca del servicio de búsqueda de Microsoft Azure"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Microsoft Azure Search: preguntas más frecuentes (P+F)
 
 Busque respuestas toocommonly preguntas más frecuentes sobre conceptos, código y los escenarios relacionados con tooAzure búsqueda.

## <a name="platform"></a>Plataforma

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>¿En qué se diferencia la búsqueda de texto completo en DBMS de la de Azure Search?

Azure Search admite varios orígenes de datos, el [análisis lingüístico en muchos lenguajes](https://docs.microsoft.com/rest/api/searchservice/language-support), [análisis personalizados para entradas de datos interesantes e inusuales](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), controles del rango de búsqueda a través de [perfiles de puntuación](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) y características de la experiencia del usuario como la escritura anticipada, el resaltado de referencias y la navegación por facetas. También incluye otras características, como los sinónimos y la sintaxis de consulta completa, pero no suelen ser relevantes.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>¿Cuál es la diferencia de hello entre la búsqueda de Azure y Elasticsearch?

Cuando se comparan las tecnologías de búsqueda, los clientes a menudo preguntan información específica sobre Azure Search y Elasticsearch. Los clientes que decidan búsqueda de Azure sobre Elasticsearch para la búsqueda de su proyectos de aplicación suelen hacen ya que hemos realizado una tarea clave sea más fácil o que necesitan la integración incorporada de hello con otras tecnologías de Microsoft:

+ Azure Search es un servicio en la nube completamente administrado con acuerdos de nivel de servicio (SLA) del 99,9 % cuando se aprovisiona con suficiente redundancia (dos réplicas para el acceso de lectura y tres para lectura y escritura).
+ Los [procesadores de lenguaje Natural](https://docs.microsoft.com/rest/api/searchservice/language-support) de Microsoft ofrecen un análisis lingüístico puntero.  
+ Los [indexadores de Azure Search](search-indexer-overview.md) pueden rastrear diversos orígenes de datos de Azure para llevar a cabo la indexación inicial e incremental.
+ Si necesita toofluctuations de respuesta rápida en la consulta o indizar volúmenes, puede usar [controles deslizantes](search-manage.md#scale-up-or-down) en hello Azure portal o ejecutar un [script de PowerShell](search-manage-powershell.md), omitiendo la administración de particiones directamente.  
+ [Características de optimización y la puntuación de](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) proporcionan Hola significa para influir en puntuaciones de clasificación de búsqueda más allá de qué motor de búsqueda de hello independiente puede proporcionar. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>¿Se puede pausar el servicio Azure Search y dejar de facturar?

No se puede pausar el servicio de Hola. Cuando se crea el servicio de hello, se asignan recursos de cálculo y almacenamiento para su uso exclusivo. No es posible toorelease y reclamar los recursos a petición. 

## <a name="indexing-operations"></a>Operaciones de indexación

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>¿Índices de copia de seguridad y restauración (o de descarga y movimiento ) o instantáneas de índices?

Aunque puede [para obtener una definición de índice](https://docs.microsoft.com/rest/api/searchservice/get-index) en cualquier momento, no hay ningún índice extracción, instantánea o la característica de restauración de copia de seguridad para la descarga de un *rellena* índice que se ejecuta en el sistema local de hello en la nube tooa, o moverlo tooanother servicio de búsqueda de Azure. 

Se generan índices y se rellenan desde el código que se escribe y ejecuta solo en la búsqueda de Azure en la nube de Hola. Por lo general, los clientes que desean toomove un tooanother de servicios de index Server hacerlo editando su toouse código un nuevo punto de conexión y, a continuación, vuelva a ejecutar la indización. Si desea Hola capacidad tootake una instantánea o un índice de la copia de seguridad, se debe convertir un voto [User Voice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>¿Se puede indizar de réplicas de bases de datos SQL (se aplica demasiado[indizadores de base de datos de SQL Azure](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 No hay ninguna restricción en el uso de Hola de réplicas principal o secundaria como un origen de datos al crear un índice desde el principio. Sin embargo, la actualización de un índice con actualizaciones incrementales (basadas en los registros modificados) requiere réplica principal de Hola. Este requisito procede de SQL Database, que garantiza el seguimiento de los cambios solo en las réplicas principales. Si intenta usar las réplicas secundarias para una carga de trabajo de actualización de índice, no hay ninguna garantía que obtener todos los datos de Hola.

## <a name="search-operations"></a>Operaciones de búsqueda

### <a name="can-i-search-across-multiple-indexes"></a>¿Se puede buscar en varios índices?

No, esta operación no se admite. Búsqueda nunca distingue tooa ámbito único índice.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>¿Se puede restringir el acceso al corpus de búsqueda según la identidad del usuario?

Azure Search no tiene un modelo de seguridad basada en roles para el acceso a los datos por usuario. La autenticación es cualquier derechos completos o de solo lectura en el nivel del servicio de Hola. Algunos clientes han implementado soluciones basadas en el [parámetro de búsqueda `$filter`](https://docs.microsoft.com/rest/api/searchservice/search-documents), pero solo es una solución alternativa. Si desea esta característica, vote en [User Voice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>¿Por qué hay cero coincidencias en términos que toobe válida se puede saber?

caso más habitual de Hello no consiste en saber que cada tipo de consulta es compatible con los niveles de análisis lingüísticos y comportamientos de búsqueda diferentes. Búsqueda de texto completo, que es la carga de trabajo predominante hello, incluye una fase de análisis de lenguaje que perjudique términos hacia abajo tooroot formularios. Este aspecto del análisis de la consulta proyecta una red más amplia sobre posibles coincidencias, porque hello con tokens término coincide con un número mayor de variantes.

Si invoca [otros tipos de consultas](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (búsqueda con comodín, búsqueda aproximada, búsqueda de proximidad, sugerencias, entre otras), no hay ningún análisis lingüístico. Términos se agregan el árbol de la consulta toohello como-es. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>¿Por qué es una puntuación igual o constante de 1.0 para cada acierto clasificación hello en las búsquedas?

De forma predeterminada, los resultados de búsqueda reciben una puntuación basada en hello [propiedades estadísticas de términos de búsqueda de coincidencias](search-lucene-query-architecture.md#stage-4-scoring)y ordenar toolow alta Hola conjunto de resultados. Sin embargo, algunas consultas tipos (comodín, el prefijo y regex) siempre aporta una puntuación constante toohello general de puntuación de documentos. Este comportamiento es así por diseño. Búsqueda de Azure impone una constante puntuación coincidencias tooallow se encuentran a través de toobe de expansión de consulta incluido en los resultados de hello, sin afectar a la clasificación de Hola. 

Por ejemplo, suponga que la entrada "pase*" en una búsqueda con caracteres comodín genera coincidencias en "pasear", "paseo" y "paseante". Dada la naturaleza de Hola de estos resultados, no hay ninguna manera tooreasonably deducir cuáles son los términos son más valiosos que otros usuarios. Por este motivo, se omiten las frecuencias de los términos cuando se realiza la puntuación de los resultados en consultas de los tipos caracteres comodín, prefijo y regex. Resultados de la búsqueda en función de una entrada parcial se proporcionan una constante puntuación tooavoid sesgo hacia coincidencias potencialmente inesperadas.

## <a name="design-patterns"></a>Patrones de diseño

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>¿Cuál es el mejor método para implementar la búsqueda localizada de hello?

Mayoría de los clientes elegir campos dedicadas en una colección cuando se trata de toosupporting distintas configuraciones regionales (idiomas) Hola mismo índice. Campos específicos de la configuración regional que sea posible tooassign un analizador adecuado. Por ejemplo, asignación de campo de tooa de hello analizador de francés de Microsoft que contiene cadenas en francés. También simplifica el filtrado. Si sabe que una consulta se inicia en una página de fr-fr, podría limitar el campo de toothis de resultados de búsqueda. O bien, crear un [perfil de puntuación](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive Hola campo más peso relativo.

## <a name="next-steps"></a>Pasos siguientes

¿Es su pregunta acerca de una característica o funcionalidad que falta? Solicitar característica hello en hello [sitio web de User Voice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Otras referencias

 [StackOverflow: Azure Search](https://stackoverflow.com/questions/tagged/azure-search)   
 [Cómo funciona la búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md)  
 [¿Qué es Azure Search?](search-what-is-azure-search.md)

 