---
title: "aaaHow toouse Fiddler tooevaluate y pruebe la API de REST de búsqueda de Azure | Documentos de Microsoft"
description: "Utilizar Fiddler para una disponibilidad de búsqueda de Azure tooverifying enfoque sin código y probar hello las API de REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Utilizar Fiddler tooevaluate y pruebe la API de REST de búsqueda de Azure
> [!div class="op_single_selector"]
>
> * [Información general](search-query-overview.md)
> * [Explorador de búsqueda](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Este artículo se explica cómo toouse Fiddler, disponible como un [descarga gratuita de Telerik](http://www.telerik.com/fiddler), tooissue HTTP solicitudes tooand ver respuestas mediante Hola API de REST de búsqueda de Azure, sin tener que toowrite cualquier código. Búsqueda de Azure es un servicio de búsqueda hospedado en la nube en Microsoft Azure, fácilmente programable a través de API de .NET y REST. Hola las API de REST se documentan en el servicio de búsqueda de Azure [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

Hola pasos, podrá crear un índice, cargar documentos, índice de Hola de consulta y, a continuación, consultar el sistema de Hola para obtener información de servicio.

toocomplete estos pasos, necesitará un servicio de búsqueda de Azure y `api-key`. Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener instrucciones sobre cómo iniciar tooget.

## <a name="create-an-index"></a>Creación de un índice
1. Inicie Fiddler. En hello **archivo** menú, desactive la opción **capturar tráfico** actividad HTTP extraño toohide es toohello no relacionados de tarea actual.
2. En hello **compositor** ficha, podrá formular una solicitud similar Hola siguiente captura de pantalla.

      ![][1]
3. Seleccione **PUT**.
4. Escriba una dirección URL que especifica la dirección URL del servicio de hello, atributos de la solicitud y Hola api-version. Unos tookeep de punteros en cuenta:

   * Use HTTPS como prefijo de Hola.
   * El atributo de solicitud es "/índices/hoteles". Esto indica que la búsqueda toocreate a un índice con el nombre 'hoteles'.
   * La versión de la API se escribe en minúsculas y se especifica como "?api-version=2016-09-01". Las versiones de API son importantes porque Búsqueda de Azure implementa actualizaciones regularmente. En raras ocasiones, una actualización de servicio puede introducir un toohello de cambio de separación de API. Por este motivo, Búsqueda de Azure requiere una versión de la API en cada solicitud para que tenga el control total sobre cuál se usa.

     dirección URL completa de Hello debería ser similar toohello siguiente ejemplo.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Especificar el encabezado de solicitud de hello, reemplazando los host de Hola y clave de api con valores que son válidos para el servicio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. En el cuerpo de solicitud, pegue en los campos de Hola que componen la definición del índice Hola.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. Haga clic en **Ejecutar**.

En unos segundos, debería ver una respuesta HTTP 201 en la lista de sesiones de hello, índice de Hola que indica que se creó correctamente.

Si obtiene HTTP 504, compruebe la que dirección URL de hello especifique HTTPS. Si ve HTTP 400 o 404, compruebe solicitud hello tooverify de cuerpo no existe, se produjeron errores copiar y pegar. Un HTTP 403 normalmente indica un problema con hello clave de api (una clave no válida o un problema de sintaxis con cómo se especifica la clave de api de hello).

## <a name="load-documents"></a>Carga de documentos
En hello **compositor** ficha, los documentos de toopost solicitud será similar a Hola siguiente. cuerpo de saludo de solicitud de hello contiene datos de búsqueda de Hola de 4 hoteles.

   ![][2]

1. Seleccione **POST**.
2. Escriba una URL que comience con HTTPS, seguida de la URL del servicio y, después, "/indexes/<'indexname'>/docs/index?api-version=2016-09-01". dirección URL completa de Hello debería ser similar toohello siguiente ejemplo.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. Encabezado de solicitud debe ser Hola mismo que antes. Recuerde que reemplaza host hello y clave de api con valores que son válidos para el servicio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hola cuerpo de solicitud contiene el índice de cuatro documentos toobe toohello agregado hoteles.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. Haga clic en **Ejecutar**.

En unos segundos, debería ver una respuesta HTTP 200 en la lista de sesiones de Hola. Esto indica Hola documentos se crearon correctamente. Si se produce un 207, al menos un documento no pudo tooupload. Si se produce un error 404, tiene un error de sintaxis en el encabezado de Hola o cuerpo de solicitud de saludo.

## <a name="query-hello-index"></a>Índice de Hola de consulta
Ahora que se han cargado el índice y los documentos, puede emitir consultas con ellos.  En hello **compositor** ficha, una **obtener** comando que consulta el servicio tendrá un aspecto similar toohello siguiente captura de pantalla.

   ![][3]

1. Seleccione **GET**.
2. Escriba una URL que comience por HTTPS, seguida de la URL del servicio, después "/indexes/<'indexname'>/docs?" y, después, los parámetros de la consulta. Por ejemplo, usar hello después de la dirección URL, reemplazando el nombre de host de ejemplo de Hola con uno que sea válido para el servicio.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Esta consulta busca Hola término "motel" y recupera las categorías de faceta de clasificaciones.
3. Encabezado de solicitud debe ser Hola mismo que antes. Recuerde que reemplaza host hello y clave de api con valores que son válidos para el servicio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

código de respuesta de Hello debería ser 200 y salida de respuesta de hello debe tener un aspecto similar toohello siguiente captura de pantalla.

   ![][4]

Hola consulta de ejemplo siguiente es de hello [operación de índice de búsqueda (API de búsqueda de Azure)](http://msdn.microsoft.com/library/dn798927.aspx) en MSDN. Muchas de las consultas de ejemplo de Hola en este tema incluyen espacios, que no se permiten en Fiddler. Reemplazar cada espacio con un carácter + antes de pegar Hola la cadena de consulta antes de intentar consulta hello en Fiddler.

**Los espacios anteriores se reemplazan:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Los espacios posteriores se reemplazan por +:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>Consultar el sistema Hola
También puede consultar Hola sistema tooget recuentos y almacenamiento consumo de documento. En hello **compositor** ficha, tendrá un aspecto similar siguiente toohello su solicitud y respuesta de hello devolverá un recuento para el número de Hola de documentos y el espacio utilizado.

 ![][5]

1. Seleccione **GET**.
2. Escriba una URL que incluya la URL de su servicio, seguida de "/indexes/hotels/stats?api-version=2016-09-01":

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Especificar el encabezado de solicitud de hello, reemplazando los host de Hola y clave de api con valores que son válidos para el servicio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Deje en blanco cuerpo de la solicitud de saludo.
5. Haga clic en **Ejecutar**. Debería ver un código de estado HTTP 200 en la lista de sesiones de Hola. Seleccione la entrada de hello registrado para el comando.
6. Haga clic en hello **inspectores** , haga clic en hello **encabezados** ficha y formato JSON, a continuación, seleccione Hola. Debería ver el tamaño de almacenamiento y el recuento del documento de hello (en KB).

## <a name="next-steps"></a>Pasos siguientes
Vea [administrar el servicio de búsqueda en Azure](search-manage.md) para un enfoque sin código toomanaging y usar búsqueda de Azure.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
