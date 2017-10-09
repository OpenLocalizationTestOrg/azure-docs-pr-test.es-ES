---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentación preliminar de característica de sinónimos (vista previa) de hello, expuesta en hello API de REST de búsqueda de Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Sinónimos en Azure Search (versión preliminar)

Sinónimos en los motores de búsqueda asocian términos equivalentes que se expanden implícitamente ámbito Hola de una consulta, sin que el usuario de hello tener tooactually proporcionar término Hola. Por ejemplo, hello determinado término "dog" y las asociaciones de sinónimos de "perro" y "cachorro", todos los documentos que contengan "dog", "perro" o "cachorro" entrarán en ámbito de Hola de consulta de Hola.

En Azure Search, la expansión de sinónimos se realiza en el momento de la consulta. Puede agregar sinónimo mapas tooa servicio con ninguna operación de tooexisting de interrupción. Puede agregar un **synonymMaps** definición de campo de propiedad tooa sin necesidad de índice de hello toorebuild. Para más información, vea [Actualización de índice](https://docs.microsoft.com/rest/api/searchservice/update-index).

## <a name="feature-availability"></a>Disponibilidad de características

sinónimos de Hello característica está actualmente en vista previa y solo es compatible en Hola versión de api de vista previa más reciente (api-version = 2016-09-01-versión preliminar). En este momento no es compatible con Azure Portal. Porque se especifica la versión de API de hello en solicitud de hello, es posible toocombine disponible con carácter general (GA) y API de vista previa en hello misma aplicación. Sin embargo, la versión preliminar de las API no se someten a las condiciones del Acuerdo de Nivel de Servicio y sus características pueden cambiar, por lo que no se recomienda su uso en aplicaciones de producción.

## <a name="how-toouse-synonyms-in-azure-search"></a>Cómo buscar sinónimos toouse en Azure

En búsqueda de Azure, compatibilidad con sinónimos se basa en los mapas de sinónimo que define y cargar el servicio tooyour. Estas asignaciones constituyen un recurso independiente (como índices u orígenes de datos), y cualquier campo buscable puede usarlas en cualquier índice en el servicio de búsqueda.

Los índices y asignaciones de sinónimos se mantienen de forma independiente. Una vez que se define un mapa de sinónimo y cargarlo tooyour servicio, puede habilitar característica de sinónimo de hello en un campo mediante la adición de una nueva propiedad llamada **synonymMaps** en la definición de campo de Hola. Crear, actualizar y eliminar que una asignación de sinónimo siempre es una operación de documento de enteros, lo que significa que no se puede crear, actualización o eliminen elementos de mapa de sinónimo Hola incrementalmente. La actualización de incluso una entrada única requiere que se vuelva a cargar.

La incorporación de sinónimos en la aplicación de búsqueda es un proceso de dos pasos:

1.  Agregar un servicio de búsqueda de sinónimo mapa tooyour a través de las API debajo de Hola.  

2.  Configurar una asignación de campo de búsqueda toouse Hola sinónimo en la definición del índice Hola.

### <a name="synonymmaps-resource-apis"></a>API de recursos de SynonymMaps

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Adición o actualización de una asignación de sinónimos en su servicio, con POST o PUT

Mapas de sinónimo se cargan toohello servicio a través de POST o PUT. Cada regla debe estar delimitado por el carácter de nueva línea ('\n') de Hola. Puede definir too5, 000 reglas por asignación sinónimo en un servicio gratuito y 10 000 reglas en todas las SKU que otros. Cada regla puede tener hasta too20 expansiones.

En esta versión preliminar, mapas de sinónimo deben tener formato de Apache Solr Hola que se explica a continuación. Si tiene un diccionario de sinónimos existentes en un formato diferente y desea toouse lo directamente, háganoslo saber en [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

Puede crear un nuevo mapa de sinónimo utilizando HTTP POST, como en el siguiente ejemplo de Hola:

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

Como alternativa, puede usar PUT y especifique el nombre de asignación de sinónimo de hello en hello URI. Si el mapa de sinónimo hello no existe, se creará.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Formato de sinónimos de Apache

formato de Hello Solr admite asignaciones de sinónimo equivalente y explícita. Las reglas de asignación cumplen la especificación del filtro sinónimo toohello de código abierto de Apache Solr, se describe en este documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). A continuación se muestra una regla de ejemplo para los sinónimos equivalentes.
```
              USA, United States, United States of America
```

Con la regla de hello anterior, una consulta de búsqueda "EE" expandirá demasiado "EE" o "United States" o "Estados Unidos".

La asignación explícita se denota mediante una flecha "=>". Cuando especifica una secuencia de términos de una consulta de búsqueda que coincide con hello del lado izquierdo de "= >" se reemplazará con alternativas de hello en hello del lado derecho. Dada la regla de Hola a continuación, las consultas de búsqueda "Washington", "Washington" o "WA" todos se reescribirán demasiado "WA". Asignación explícita solo se aplica en la dirección de hello especificada y no vuelva a escribir consultas de Hola "WA" demasiado "Washington" en este caso.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Enumeración de asignaciones de sinónimos en su servicio

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Obtención de la asignación de sinónimos en su servicio

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Eliminación de la asignación de sinónimos en su servicio

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Configurar una asignación de campo de búsqueda toouse Hola sinónimo en la definición del índice Hola.

Una nueva propiedad de campo **synonymMaps** puede ser usado toospecify un toouse de mapa de sinónimo para un campo de búsqueda. Las asignaciones de sinónimo son recursos de nivel de servicio y pueden hacer referencia a cualquier campo de un índice mediante el servicio Hola.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** se puede especificar para campos de búsqueda de tipo hello 'Edm.String' o 'Collection (EDM.String)'.

> [!NOTE]
> En esta versión preliminar, solo puede tener una asignación de sinónimos por campo. Si desea toouse varias asignaciones de sinónimo, háganoslo saber en [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Repercusión de Sinónimos en otras características de búsqueda

característica de sinónimos de Hello reescribe la consulta original de hello con sinónimos con hello operador OR. Por esta razón, resaltado de llamadas y los perfiles de puntuación tratan término original de Hola y sinónimos como equivalentes.

Característica de sinónimo aplica a las consultas de toosearch y no hay ningún toofilters o facetas. De forma similar, las sugerencias se basan únicamente en términos de hello original; coincidencias de sinónimos no aparecen en la respuesta de Hola.

Expansiones de sinónimo no aplican los términos de búsqueda toowildcard; no se expanden prefijo, de forma aproximada y los términos de regex.

## <a name="tips-for-building-a-synonym-map"></a>Consejos para crear un asignación de sinónimos

- Una asignación de sinónimos concisa y bien diseñada es más eficiente que una lista exhaustiva de posibles coincidencias. Diccionarios excesivamente grandes o complejos tardar más tiempo tooparse y afecta a la latencia de consulta Hola si consulta Hola expande toomany sinónimos. En lugar de estimación en el que podrían utilizarse términos, puede obtener términos real de Hola a través de un [buscar informes de análisis de tráfico](search-traffic-analytics.md).

- Como ejercicio un preliminar y la validación, habilitar y, a continuación, use este informe tooprecisely determinar cuáles son los términos beneficiarse de una coincidencia de sinónimo y, a continuación, continuar toouse como que la asignación de sinónimo produce mejores resultados de validación. En el informe de hello predefinido, Hola iconos "consultas de búsqueda más comunes" e "consultas de búsqueda de resultado de cero" le proporcionará la información necesaria de Hola.

- Puede crear varias asignaciones para la aplicación de búsqueda (por ejemplo, mediante el idioma si la aplicación es compatible con una base de cliente de varios idiomas). Actualmente, un campo solo puede usar una de ellas. Puede actualizar una propiedad synonymMaps del campo en cualquier momento.

## <a name="next-steps"></a>Pasos siguientes

- Si tiene un índice existente en un entorno de desarrollo (no es de producción), experimentar con un pequeño diccionario toosee cómo cambia la experiencia de búsqueda de hello, incluido el impacto en los perfiles de puntuación, posicionamiento resaltado y sugerencias suma Hola de sinónimos.

- [Habilitar el análisis de tráfico de búsqueda](search-traffic-analytics.md) y use Hola predefinidos toolearn qué términos se usan Hola mayoría y los que los devuelto cero documentos de informe de Power BI. Gracias a estas informaciones, revise los sinónimos de tooinclude de diccionario de Hola para consultas improductivos que deberían estar resolviendo toodocuments en el índice.
