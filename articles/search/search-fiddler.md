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
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="a402a-103">Utilizar Fiddler tooevaluate y pruebe la API de REST de búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a402a-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="a402a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a402a-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="a402a-105">Explorador de búsqueda</span><span class="sxs-lookup"><span data-stu-id="a402a-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="a402a-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="a402a-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="a402a-107">.NET</span><span class="sxs-lookup"><span data-stu-id="a402a-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="a402a-108">REST</span><span class="sxs-lookup"><span data-stu-id="a402a-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="a402a-109">Este artículo se explica cómo toouse Fiddler, disponible como un [descarga gratuita de Telerik](http://www.telerik.com/fiddler), tooissue HTTP solicitudes tooand ver respuestas mediante Hola API de REST de búsqueda de Azure, sin tener que toowrite cualquier código.</span><span class="sxs-lookup"><span data-stu-id="a402a-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="a402a-110">Búsqueda de Azure es un servicio de búsqueda hospedado en la nube en Microsoft Azure, fácilmente programable a través de API de .NET y REST.</span><span class="sxs-lookup"><span data-stu-id="a402a-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="a402a-111">Hola las API de REST se documentan en el servicio de búsqueda de Azure [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="a402a-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="a402a-112">Hola pasos, podrá crear un índice, cargar documentos, índice de Hola de consulta y, a continuación, consultar el sistema de Hola para obtener información de servicio.</span><span class="sxs-lookup"><span data-stu-id="a402a-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="a402a-113">toocomplete estos pasos, necesitará un servicio de búsqueda de Azure y `api-key`.</span><span class="sxs-lookup"><span data-stu-id="a402a-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="a402a-114">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener instrucciones sobre cómo iniciar tooget.</span><span class="sxs-lookup"><span data-stu-id="a402a-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="a402a-115">Creación de un índice</span><span class="sxs-lookup"><span data-stu-id="a402a-115">Create an index</span></span>
1. <span data-ttu-id="a402a-116">Inicie Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a402a-116">Start Fiddler.</span></span> <span data-ttu-id="a402a-117">En hello **archivo** menú, desactive la opción **capturar tráfico** actividad HTTP extraño toohide es toohello no relacionados de tarea actual.</span><span class="sxs-lookup"><span data-stu-id="a402a-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="a402a-118">En hello **compositor** ficha, podrá formular una solicitud similar Hola siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a402a-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="a402a-119">Seleccione **PUT**.</span><span class="sxs-lookup"><span data-stu-id="a402a-119">Select **PUT**.</span></span>
4. <span data-ttu-id="a402a-120">Escriba una dirección URL que especifica la dirección URL del servicio de hello, atributos de la solicitud y Hola api-version.</span><span class="sxs-lookup"><span data-stu-id="a402a-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="a402a-121">Unos tookeep de punteros en cuenta:</span><span class="sxs-lookup"><span data-stu-id="a402a-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="a402a-122">Use HTTPS como prefijo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a402a-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="a402a-123">El atributo de solicitud es "/índices/hoteles".</span><span class="sxs-lookup"><span data-stu-id="a402a-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="a402a-124">Esto indica que la búsqueda toocreate a un índice con el nombre 'hoteles'.</span><span class="sxs-lookup"><span data-stu-id="a402a-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="a402a-125">La versión de la API se escribe en minúsculas y se especifica como "?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="a402a-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="a402a-126">Las versiones de API son importantes porque Búsqueda de Azure implementa actualizaciones regularmente.</span><span class="sxs-lookup"><span data-stu-id="a402a-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="a402a-127">En raras ocasiones, una actualización de servicio puede introducir un toohello de cambio de separación de API.</span><span class="sxs-lookup"><span data-stu-id="a402a-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="a402a-128">Por este motivo, Búsqueda de Azure requiere una versión de la API en cada solicitud para que tenga el control total sobre cuál se usa.</span><span class="sxs-lookup"><span data-stu-id="a402a-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="a402a-129">dirección URL completa de Hello debería ser similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a402a-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="a402a-130">Especificar el encabezado de solicitud de hello, reemplazando los host de Hola y clave de api con valores que son válidos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a402a-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="a402a-131">En el cuerpo de solicitud, pegue en los campos de Hola que componen la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="a402a-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

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
7. <span data-ttu-id="a402a-132">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a402a-132">Click **Execute**.</span></span>

<span data-ttu-id="a402a-133">En unos segundos, debería ver una respuesta HTTP 201 en la lista de sesiones de hello, índice de Hola que indica que se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="a402a-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="a402a-134">Si obtiene HTTP 504, compruebe la que dirección URL de hello especifique HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a402a-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="a402a-135">Si ve HTTP 400 o 404, compruebe solicitud hello tooverify de cuerpo no existe, se produjeron errores copiar y pegar.</span><span class="sxs-lookup"><span data-stu-id="a402a-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="a402a-136">Un HTTP 403 normalmente indica un problema con hello clave de api (una clave no válida o un problema de sintaxis con cómo se especifica la clave de api de hello).</span><span class="sxs-lookup"><span data-stu-id="a402a-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="a402a-137">Carga de documentos</span><span class="sxs-lookup"><span data-stu-id="a402a-137">Load documents</span></span>
<span data-ttu-id="a402a-138">En hello **compositor** ficha, los documentos de toopost solicitud será similar a Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="a402a-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="a402a-139">cuerpo de saludo de solicitud de hello contiene datos de búsqueda de Hola de 4 hoteles.</span><span class="sxs-lookup"><span data-stu-id="a402a-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="a402a-140">Seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="a402a-140">Select **POST**.</span></span>
2. <span data-ttu-id="a402a-141">Escriba una URL que comience con HTTPS, seguida de la URL del servicio y, después, "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="a402a-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="a402a-142">dirección URL completa de Hello debería ser similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a402a-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="a402a-143">Encabezado de solicitud debe ser Hola mismo que antes.</span><span class="sxs-lookup"><span data-stu-id="a402a-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="a402a-144">Recuerde que reemplaza host hello y clave de api con valores que son válidos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a402a-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="a402a-145">Hola cuerpo de solicitud contiene el índice de cuatro documentos toobe toohello agregado hoteles.</span><span class="sxs-lookup"><span data-stu-id="a402a-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

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
5. <span data-ttu-id="a402a-146">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a402a-146">Click **Execute**.</span></span>

<span data-ttu-id="a402a-147">En unos segundos, debería ver una respuesta HTTP 200 en la lista de sesiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a402a-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="a402a-148">Esto indica Hola documentos se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="a402a-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="a402a-149">Si se produce un 207, al menos un documento no pudo tooupload.</span><span class="sxs-lookup"><span data-stu-id="a402a-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="a402a-150">Si se produce un error 404, tiene un error de sintaxis en el encabezado de Hola o cuerpo de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="a402a-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="a402a-151">Índice de Hola de consulta</span><span class="sxs-lookup"><span data-stu-id="a402a-151">Query hello index</span></span>
<span data-ttu-id="a402a-152">Ahora que se han cargado el índice y los documentos, puede emitir consultas con ellos.</span><span class="sxs-lookup"><span data-stu-id="a402a-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="a402a-153">En hello **compositor** ficha, una **obtener** comando que consulta el servicio tendrá un aspecto similar toohello siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a402a-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="a402a-154">Seleccione **GET**.</span><span class="sxs-lookup"><span data-stu-id="a402a-154">Select **GET**.</span></span>
2. <span data-ttu-id="a402a-155">Escriba una URL que comience por HTTPS, seguida de la URL del servicio, después "/indexes/<'indexname'>/docs?" y, después, los parámetros de la consulta.</span><span class="sxs-lookup"><span data-stu-id="a402a-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="a402a-156">Por ejemplo, usar hello después de la dirección URL, reemplazando el nombre de host de ejemplo de Hola con uno que sea válido para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a402a-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="a402a-157">Esta consulta busca Hola término "motel" y recupera las categorías de faceta de clasificaciones.</span><span class="sxs-lookup"><span data-stu-id="a402a-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="a402a-158">Encabezado de solicitud debe ser Hola mismo que antes.</span><span class="sxs-lookup"><span data-stu-id="a402a-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="a402a-159">Recuerde que reemplaza host hello y clave de api con valores que son válidos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a402a-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="a402a-160">código de respuesta de Hello debería ser 200 y salida de respuesta de hello debe tener un aspecto similar toohello siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a402a-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="a402a-161">Hola consulta de ejemplo siguiente es de hello [operación de índice de búsqueda (API de búsqueda de Azure)](http://msdn.microsoft.com/library/dn798927.aspx) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="a402a-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="a402a-162">Muchas de las consultas de ejemplo de Hola en este tema incluyen espacios, que no se permiten en Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a402a-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="a402a-163">Reemplazar cada espacio con un carácter + antes de pegar Hola la cadena de consulta antes de intentar consulta hello en Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a402a-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="a402a-164">**Los espacios anteriores se reemplazan:**</span><span class="sxs-lookup"><span data-stu-id="a402a-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="a402a-165">**Los espacios posteriores se reemplazan por +:**</span><span class="sxs-lookup"><span data-stu-id="a402a-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="a402a-166">Consultar el sistema Hola</span><span class="sxs-lookup"><span data-stu-id="a402a-166">Query hello system</span></span>
<span data-ttu-id="a402a-167">También puede consultar Hola sistema tooget recuentos y almacenamiento consumo de documento.</span><span class="sxs-lookup"><span data-stu-id="a402a-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="a402a-168">En hello **compositor** ficha, tendrá un aspecto similar siguiente toohello su solicitud y respuesta de hello devolverá un recuento para el número de Hola de documentos y el espacio utilizado.</span><span class="sxs-lookup"><span data-stu-id="a402a-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="a402a-169">Seleccione **GET**.</span><span class="sxs-lookup"><span data-stu-id="a402a-169">Select **GET**.</span></span>
2. <span data-ttu-id="a402a-170">Escriba una URL que incluya la URL de su servicio, seguida de "/indexes/hotels/stats?api-version=2016-09-01":</span><span class="sxs-lookup"><span data-stu-id="a402a-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="a402a-171">Especificar el encabezado de solicitud de hello, reemplazando los host de Hola y clave de api con valores que son válidos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a402a-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="a402a-172">Deje en blanco cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="a402a-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="a402a-173">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a402a-173">Click **Execute**.</span></span> <span data-ttu-id="a402a-174">Debería ver un código de estado HTTP 200 en la lista de sesiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a402a-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="a402a-175">Seleccione la entrada de hello registrado para el comando.</span><span class="sxs-lookup"><span data-stu-id="a402a-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="a402a-176">Haga clic en hello **inspectores** , haga clic en hello **encabezados** ficha y formato JSON, a continuación, seleccione Hola.</span><span class="sxs-lookup"><span data-stu-id="a402a-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="a402a-177">Debería ver el tamaño de almacenamiento y el recuento del documento de hello (en KB).</span><span class="sxs-lookup"><span data-stu-id="a402a-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a402a-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a402a-178">Next steps</span></span>
<span data-ttu-id="a402a-179">Vea [administrar el servicio de búsqueda en Azure](search-manage.md) para un enfoque sin código toomanaging y usar búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="a402a-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
