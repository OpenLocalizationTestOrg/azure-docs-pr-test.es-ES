---
title: "aaaWhat es la búsqueda de Azure | Documentos de Microsoft"
description: "Azure Search es un servicio de búsqueda completamente administrado hospedado en la nube. Conozca más en la información general de esta característica."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>¿Qué es Azure Search?
Azure Search es una solución de búsqueda como servicio en la nube que ofrece a los desarrolladores las API y las herramientas necesarias para agregar una experiencia de búsqueda de datos enriquecida en las aplicaciones web, para dispositivos móviles y empresariales.

La funcionalidad se expone a través de un sencillo [API de REST](/rest/api/searchservice/) o [.NET SDK](search-howto-dotnet-sdk.md) que simplifica la complejidad inherente de Hola de tecnología de búsqueda. En suma tooAPIs, Hola portal de Azure proporciona administración y soporte técnico de la creación de prototipos. La infraestructura y la disponibilidad las administra Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Resumen de características

| Categoría | Características |
|----------|----------|
|Búsqueda de texto completo y análisis de texto | [**Búsqueda de texto completo**](search-lucene-query-architecture.md) es el principal caso de uso para la mayoría de las aplicaciones basadas en búsquedas. Las consultas se formulan con una sintaxis compatible: <br/><br/>[**Sintaxis de consulta simple**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), que ofrece operadores lógicos, de búsqueda de frase, de sufijo y de precedencia.<br/><br/>[**Sintaxis de consulta Lucene**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) es compatible con cualquier búsqueda aproximada, la búsqueda por proximidad, la priorización de términos y las expresiones regulares.| 
| Integración de datos | Los índices de Azure Search aceptan datos de cualquier origen, siempre que se envíe como estructura de datos JSON. <br/><br/> Opcionalmente, para los orígenes de datos admitidos en Azure, puede usar [ **indizadores** ](search-indexer-overview.md) tooautomatically rastreo [base de datos de SQL Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [base de datos de Azure Cosmos](search-howto-index-documentdb.md), o [almacenamiento de blobs de Azure](search-howto-indexing-azure-blob-storage.md) toosync el índice de búsqueda del contenido con el almacén de datos principal. Los indexadores de Azure Blog pueden realizar la *averiguación de documentos* para [indexar los principales formatos de archivo](search-howto-indexing-azure-blob-storage.md), incluidos los documentos de Microsoft Office, PDF y HTML. |
| Análisis de búsqueda | Los [**analizadores léxicos personalizados**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) están disponibles para las consultas de búsqueda complejas, mediante la coincidencia de fonética y expresiones regulares. |
| Compatibilidad con idiomas | [**Analizadores de lenguaje** ](https://docs.microsoft.com/rest/api/searchservice/language-support) desde Lucene, así como Microsoft del lenguaje natural procesadores disponibles en lingüística de 56 distintos idiomas toointelligently identificador específico del lenguaje como verbales, sexo, plural irregular los sustantivos (por ejemplo, ' mouse' frente a 'mice'), palabras anular un interés compuesto, separación de palabras (para los idiomas sin espacios) y mucho más. |
| Búsqueda georreferenciada | Azure Search procesa, filtra y muestra las ubicaciones geográficas de forma inteligente. Permite a los usuarios tooexplore datos en función de la proximidad de Hola de una ubicación física de búsqueda resultado tooa. [Vea este vídeo](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) o [revisar este ejemplo](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn más. |
| Características de la experiencia del usuario | En una barra de búsqueda se pueden habilitar las [**sugerencias de búsqueda**](https://docs.microsoft.com/rest/api/searchservice/suggesters) para las consultas de escritura automática. Se sugieren los documentos correspondientes en el índice a medida que los usuarios escriben entradas de búsqueda parciales. <br/><br/>La [**navegación por facetas**](https://docs.microsoft.com/azure/search/search-faceted-navigation) se habilita con un único parámetro de consulta. Búsqueda de Azure devuelve una estructura de navegación por facetas que puede utilizar como código de hello detrás de una lista de categorías, para filtrar autodirigido (por ejemplo, toofilter elementos de catálogo por intervalo de precios o marca). <br/><br/> [**Filtros** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) puede ser la navegación por facetas tooincorporate usado en la interfaz de usuario de la aplicación, mejorar la formulación de consultas y filtro en función de criterios o desarrollador-especificado por el usuario. Crear filtros mediante la sintaxis de OData de Hola.<br/><br/> [**Resaltado** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) se aplica de forma visual atting tooa palabra clave en los resultados de la búsqueda de coincidencia. Se puede elegir qué campos devuelven los fragmentos resaltados.<br/><br/>[**Ordenar** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) está disponible con varios campos a través del esquema de índice de hello y, a continuación, activar o desactivar en el momento de la consulta con un único parámetro de búsqueda.<br/><br/> [**Paginación** ](search-pagination-page-layout.md) y limitación de los resultados de búsqueda es sencilla con control de hello optimizada que la búsqueda de Azure ofrece a través de los resultados de búsqueda.  
| Relevancia | La [**puntuación simple**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) es una ventaja clave de Azure Search. Los perfiles de puntuación son relevancia toomodel usado como una función de valores de hello documentos por sí mismos. Por ejemplo, conviene productos más nuevos o con un gran descuento situado más arriba en los resultados de la búsqueda de hello tooappear de productos. También se pueden crear perfiles de puntuación mediante etiquetas para puntuaciones personalizadas, según las preferencias de búsqueda de los clientes de las que se ha hecho seguimiento y se han almacenado por separado. |
| Supervisión e informes | [**Análisis de tráfico de búsqueda** ](search-traffic-analytics.md) son recopilados y analizados toounlock visión de lo que los usuarios escriben en el cuadro de búsqueda de Hola. <br/><br/>Las métricas sobre consultas por segundo, latencia y limitación se capturan y notifican en páginas del portal sin que sea necesaria ninguna configuración adicional. También puede supervisar fácilmente el índice y los recuentos de documentos para ajustar la capacidad según sea necesario. Para más información, consulte el artículo sobre la [administración de servicios](search-manage.md). |
| Herramientas para la creación de prototipos y la inspección | En el portal de hello, puede usar hello [ **Asistente para importar datos** ](search-import-data-portal.md) tooconfigure indizadores, índice diseñador toostand un índice, y [ **buscar en el explorador** ](search-explorer.md) tootest consulta y refinar los perfiles de puntuación. También puede abrir cualquier índice tooview su esquema. |
| Infraestructura | Hola **plataforma de alta disponibilidad** garantiza una experiencia de servicio de búsqueda muy confiable. Cuando se escala correctamente, [Azure Search ofrece un contrato de nivel de servicio del 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **Totalmente administrada y escalable** como cualquier solución completa, Azure Search no requiere ninguna administración de la infraestructura en absoluto. El servicio puede ser adaptada tooyour necesidades escalando en dos dimensiones toohandle más espacio de almacenamiento de documentos, mayores cargas de consultas o ambos.

## <a name="how-it-works"></a>Cómo funciona
### <a name="step-1-provision-service"></a>Paso 1: Aprovisionar el servicio
Puede poner en marcha un servicio de búsqueda de Azure en hello [portal de Azure](https://portal.azure.com/) o a través de hello [API de administración de recursos de Azure](/rest/api/searchmanagement/). Puede elegir cualquier servicio gratuito Hola compartido con otros suscriptores, o un [niveles de pago](https://azure.microsoft.com/pricing/details/search/) que dedica recursos que usa únicamente por el servicio. Para los niveles de pago, es posible escalar un servicio en dos dimensiones: 

- Agregar toogrow réplicas que carga de la consulta pesado de toohandle de capacidad.   
- Agregar almacenamiento a toogrow particiones más documentos. 

Controlar el almacenamiento de documentos y el procesamiento de consultas por separado, con lo que podrá calibrar los recursos en función de los requisitos de producción.

### <a name="step-2-create-index"></a>Paso 2: Crear un índice
Para cargar el contenido en el que quiere realizar búsquedas, primero debe definir un índice de Azure Search. Un índice es como una tabla de base de datos que contiene los datos y puede aceptar consultas de búsqueda. Para definir Hola índice esquema toomap tooreflect Hola estructura de documentos de hello desea toosearch, toofields similar en una base de datos.

Se puede crear un esquema en hello Azure Hola portal o utilizando mediante programación [.NET SDK](search-howto-dotnet-sdk.md) o [API de REST](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Paso 3: Indizar los datos
Después de definir un índice, está contenido tooupload listo. Puede usar un modelo de inserción o de extracción.

modelo de extracción de Hello recupera datos de orígenes de datos externos. Se admite mediante *indexadores* que agilizan y automatizan diversos aspectos de la ingestión de datos, como conectarse, leer y serializar datos. Los [indexadores](/rest/api/searchservice/Indexer-operations) están disponibles para Azure Cosmos DB, Azure SQL Database, Azure Blob Storage y SQL Server hospedado en Azure Virtual Machines. Puede configurar un indexador para una actualización de datos programada o a petición.

modelo de inserción de Hola se proporciona a través de hello SDK o las API de REST, se usa para enviar el índice de tooan documentos actualizados. Puede insertar datos desde prácticamente cualquier conjunto de datos con formato JSON de Hola. Vea [agregar, actualizar o eliminar documentos](/rest/api/searchservice/addupdate-or-delete-documents) o [cómo toouse Hola .NET SDK)](search-howto-dotnet-sdk.md) para obtener instrucciones sobre cómo cargar datos.

### <a name="step-4-search"></a>Paso 4: Buscar
Después de rellenar un índice, también puede [emitir consultas de búsqueda](/rest/api/searchservice/Search-Documents) tooyour de punto de conexión de servicio mediante HTTP simple solicita con API de REST o hello .NET SDK.

## <a name="how-it-compares"></a>Comparación

Los clientes a menudo se preguntan cómo se puede comparar la [búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md) con la [búsqueda de texto completo](https://en.wikipedia.org/wiki/Full_text_search) en su producto de bases de datos. La respuesta es que las capacidades de lenguaje de búsqueda de Azure son más enriquecida y más flexibles, con compatibilidad para las consultas de Lucene, analizadores de lenguaje de Lucene y Microsoft, analizadores personalizados para las entradas especializadas fonéticos u otros datos de y Hola capacidad toomerge de varios orígenes en el índice de búsqueda de Hola. 

Otro punto de inflexión es que una solución de búsqueda direcciones experiencia de búsqueda completa Hola. Por ejemplo, podría desear tener una puntuación personalizada de los resultados, navegación por facetas para un filtrado autodirigido, resaltado de referencias y sugerencias de consulta de escritura anticipada. 

Las herramientas de supervisión y comprensión de la actividad de consulta también se pueden tener en cuenta en una decisión sobre la solución de búsqueda. Por ejemplo, Azure Search admite [búsqueda de análisis de tráfico](search-traffic-analytics.md) para métricas de porcentaje de clics, búsquedas más populares búsquedas sin clics, etc. En productos donde la búsqueda es un complemento, se verá toofind poco probable que estas características.

El uso de recursos es otro punto que se debe tener en cuenta. La búsqueda en lenguaje natural requiere a menudo un proceso intensivo. Algunos de nuestros clientes descargan tooAzure de operaciones de búsqueda búsqueda como un recursos de máquina de manera toopreserve para el procesamiento de transacciones. Externalización de búsqueda, puede ajustar fácilmente escala toomatch consulta volumen.

Una vez que haya decidido toogo con búsqueda dedicada, su decisión siguiente es entre un servicio de nube o un servidor local. Un servicio de nube es la opción adecuada de hello si desea un [solución preparada con una sobrecarga mínima y el mantenimiento y la escala ajustable](#cloud-service-advantage).

En el paradigma de la nube de hello, varios proveedores ofrecen características de comparables de línea de base, con búsqueda de texto completo y búsqueda geográfica, Hola capacidad toohandle un cierto nivel de ambigüedad en entradas de búsqueda. Normalmente, tiene un [característica especializada](#feature-drilldown), o facilidad de Hola y la simplicidad general de API, herramientas y la administración, que determina la mejor Hola.

Entre los proveedores de servicios en la nube, Azure Search es el más potente para cargas de trabajo de búsqueda de texto completo en almacenes de contenido y bases de datos de Azure, y para aplicaciones que se basan principalmente en la búsqueda para navegar por el contenido y recuperar información. Las principales ventajas incluyen:

+ Integración de datos de Azure (rastreadores) en la capa de indización de Hola
+ Azure Portal para administración central
+ Escalado, confiabilidad y disponibilidad internacional de Azure
+ Análisis lingüístico y personalizado, con analizadores para la búsqueda de texto completo en 56 idiomas
+ [Características principales comunes aplicaciones centrados en toosearch](#feature-drilldown): puntuación, facetas, sugerencias, sinónimos, búsqueda geográfica y mucho más.

> [!Note]
> orígenes de datos claras y no sea de Azure de toobe son totalmente compatibles, pero se basan en una metodología de inserción de uso más intensivo de código en lugar de indizadores. Nuestras API se puede canalizar cualquier índice de búsqueda de Azure JSON tooan de colección de documentos.

Entre nuestros clientes, esos gama más amplia de hello tooleverage capaz de características de búsqueda de Azure incluyen catálogos en línea, programas de línea de negocio y aplicaciones de la detección de documentos.

## <a name="rest-api--net-sdk"></a>API de REST | .Net SDK

Si bien muchas tareas se pueden realizar en el portal de hello, búsqueda de Azure está pensado para los desarrolladores que deseen toointegrate funcionalidad de búsqueda en aplicaciones existentes. Hola siguiendo las interfaces de programación está disponible.

|Plataforma |Descripción |
|-----|------------|
|[REST](/rest/api/searchservice/) | Comandos HTTP admitidos por cualquier plataforma de programación y lenguaje, como Xamarin, Java y JavaScript|
|[.NET SDK](search-howto-dotnet-sdk.md) | Contenedor de .NET de hello API de REST proporciona codificación eficaz en C# y Hola de otros lenguajes de código administrado como destino .NET Framework |

## <a name="free-trial"></a>Evaluación gratuita
Los suscriptores de Azure pueden [aprovisionar un servicio en el nivel gratis hello](search-create-service-portal.md).

Si no es un suscriptor, puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Obtenga créditos que puede usar para probar los servicios de Azure de pago. Después de que están usados, puede mantener la cuenta de hello y usar [liberar los servicios de Azure](https://azure.microsoft.com/free/). Nunca se cobra su tarjeta de crédito a menos que cambiar la configuración y pida toobe cobrado explícitamente.

Además, puede [activar las ventajas de suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): su suscripción a MSDN le proporciona crédito todos los meses que puede usar con servicios de Azure de pago. 

## <a name="how-tooget-started"></a>Cómo iniciar tooget

1. Crear un servicio en hello [nivel gratuito](search-create-service-portal.md).

2. Paso a paso a través de uno o varios de los tutoriales de Hola. 

  + [¿Cómo toouse Hola .NET SDK](search-howto-dotnet-sdk.md) muestra hello principal pasos en código administrado.  
  + [Introducción a la API de REST de hello](https://github.com/Azure-Samples/search-rest-api-getting-started) muestra Hola mismos pasos con hello API de REST.  
  + [Crear el primer índice en el portal de hello](search-get-started-portal.md) muestra las características integradas de indización y prototipo del portal de Hola.   

Los motores de búsqueda son controladores comunes de Hola de recuperación de información en las aplicaciones móviles, web hello y, en almacenes de datos corporativos. Búsqueda de Azure proporciona herramientas para crear un toothose similar de experiencia de búsqueda en los sitios web comerciales grandes.

En este vídeo de 9 minutos del administrador de programas Liam Cavanagh, aprenda cómo puede beneficiar a su aplicación la integración de un motor de búsqueda. Unas breves demostraciones presentan las características clave de Azure Search y el aspecto típico que tiene un flujo de trabajo. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ Los minutos 0 a 3 describen las características y los casos de uso.
+ Los minutos 3 y 4 explican el aprovisionamiento del servicio. 
+ 4 a 6 minutos cubre toocreate de importar datos Asistente que se utiliza un índice mediante el conjunto de datos de hello inmobiliaria integrados.
+ Los minutos 6 a 9 muestran el Explorador de búsquedas y varias consultas.


