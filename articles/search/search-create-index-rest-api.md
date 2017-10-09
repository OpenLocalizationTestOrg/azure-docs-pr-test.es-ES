---
title: "aaa \"crear un índice (API de REST - búsqueda de Azure) | Documentos de Microsoft\""
description: "Crear un índice en el código mediante Hola API de REST de HTTP de búsqueda de Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Crear un índice de búsqueda de Azure usando Hola API de REST
> [!div class="op_single_selector"]
>
> * [Información general](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

En este artículo le guiará a través del proceso de Hola de creación de una búsqueda de Azure [índice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) utilizando Hola API de REST de búsqueda de Azure.

Antes de seguir con esta guía y crear un índice, debe haber [creado ya un servicio de Búsqueda de Azure](search-create-service-portal.md).

toocreate un índice de búsqueda de Azure mediante la API de REST de hello, emitirá una sola HTTP POST solicitud tooyour búsqueda de Azure dirección URL del extremo del servicio. La definición del índice se ubicará en el cuerpo de la solicitud de hello como contenido JSON con formato correcto.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificación de la clave de API de administración del servicio de Búsqueda de Azure
Ahora que ha aprovisionado un servicio de búsqueda de Azure, puede emitir solicitudes HTTP en el punto de conexión de su servicio en la dirección URL mediante Hola API de REST. *Todos los* las solicitudes de API deben incluir Hola clave de api que se generó Hola aprovisionar el servicio de búsqueda. Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.

1. toofind debe iniciar sesión en Hola de claves de api de su servicio [portal de Azure](https://portal.azure.com/)
2. Vaya hoja del servicio de búsqueda de Azure tooyour
3. Haga clic en hello icono "Claves"

El servicio tendrá *claves de administración* y *claves de consulta*.

* El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos. Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.
* Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.

Para fines de Hola de creación de un índice, puede usar su clave de administración principal o secundaria.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Definición del índice de Búsqueda de Azure mediante JSON con formato correcto
Un único servicio de tooyour de solicitud HTTP POST creará el índice. cuerpo de saludo de la solicitud HTTP POST contendrá un único objeto JSON que define el índice de búsqueda de Azure.

1. Hola primera propiedad de este objeto JSON es nombre Hola de su índice.
2. Hola segunda propiedad de este objeto JSON es una matriz JSON denominada `fields` que contiene un objeto JSON independiente para cada campo en el índice. Cada uno de estos objetos JSON contener varios pares de nombre/valor para cada uno de los atributos de campo de un hello como "name", "tipo", etcetera.

Es importante mantener sus necesidades de negocio y experiencia de usuario de búsqueda en cuenta al diseñar el índice como cada campo debe estar asignado hello [atributos propios](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Estos atributos controlan el que buscar características (filtrado, facetas, ordenación, búsqueda de texto completo, etc.) se aplican toowhich campos. Para cualquier atributo que no se especifica, valor predeterminado de hello es característica de búsqueda de tooenable Hola correspondiente a menos que se deshabilite específicamente.

En nuestro ejemplo, hemos llamado a nuestro índice "hoteles" y definido los campos como sigue:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Cuidadosamente que hemos elegido atributos de índice de Hola para cada campo en función de cómo creemos que se usarán en una aplicación. Por ejemplo, `hotelId` es una clave única que busca hoteles es probable que no conoce, por lo que se deshabilita la búsqueda de texto completo para ese campo estableciendo las personas `searchable` demasiado`false`, lo que ahorra espacio en el índice de Hola.

Tenga en cuenta que exactamente un campo en el índice de tipo `Edm.String` debe designarse como campo de 'key' Hola Hola.

definición del índice Hola anterior utiliza un analizador de lenguaje para hello `description_fr` campo porque está previsto toostore texto en francés. Vea [tema de compatibilidad de lenguaje de hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) , así como la correspondiente hello [entrada de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) para obtener más información acerca de analizadores de lenguaje.

## <a name="issue-hello-http-request"></a>Solicitud del problema Hola HTTP
1. Si usa la definición del índice como cuerpo de la solicitud de hello, emitir una dirección URL del extremo HTTP POST solicitud tooyour búsqueda de Azure servicio. En dirección URL de hello, se toouse seguro el nombre del servicio como nombre de host de hello y, empezar Hola apropiado `api-version` como un parámetro de cadena de consulta (es la versión actual de la API de hello `2016-09-01` en tiempo de hello sobre la publicación de este documento).
2. En los encabezados de solicitud hello, especifique hello `Content-Type` como `application/json`. También necesitará tooprovide clave de administración de su servicio en la que ha identificado en el paso I en hello `api-key` encabezado.

Deberá tooprovide su propio nombre y la api tooissue clave Hola solicitud de servicio a continuación:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Para una solicitud correcta, debería ver el código de estado "201 (Created)". Para obtener más información acerca de cómo crear un índice a través de la API de REST de hello, visite hello [referencia de la API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Para más información sobre otros códigos de estado HTTP que se devuelven en caso de error, consulte [Códigos de estado HTTP (Búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Cuando haya terminado con un índice y quiere toodelete lo, simplemente emita una solicitud HTTP DELETE. Por ejemplo, se trata cómo se eliminaría el índice de "hoteles" hello:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Pasos siguientes
Después de crear un índice de búsqueda de Azure, estará listo demasiado[cargar su contenido en el índice de hello](search-what-is-data-import.md) para que pueda empezar a buscar los datos.
