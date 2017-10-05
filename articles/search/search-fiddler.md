---
title: "Cómo usar Fiddler para evaluar y probar las API de REST de Azure Search | Microsoft Docs"
description: "Usar Fiddler para comprobar la disponibilidad de Búsqueda de Azure y probar las API de REST sin código."
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
ms.openlocfilehash: c38b73fa69bee34ce2434c6274cb017c99ef3c35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="a9357-103">Usar Fiddler para evaluar y probar las API de REST de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a9357-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="a9357-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a9357-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="a9357-105">Explorador de búsqueda</span><span class="sxs-lookup"><span data-stu-id="a9357-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="a9357-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="a9357-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="a9357-107">.NET</span><span class="sxs-lookup"><span data-stu-id="a9357-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="a9357-108">REST</span><span class="sxs-lookup"><span data-stu-id="a9357-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="a9357-109">En este procedimiento se explica cómo usar Fiddler, disponible como [descarga gratuita de Telerik](http://www.telerik.com/fiddler), para emitir solicitudes HTTP y ver las respuestas usando la API de REST de Búsqueda de Azure sin tener que escribir código.</span><span class="sxs-lookup"><span data-stu-id="a9357-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="a9357-110">Búsqueda de Azure es un servicio de búsqueda hospedado en la nube en Microsoft Azure, fácilmente programable a través de API de .NET y REST.</span><span class="sxs-lookup"><span data-stu-id="a9357-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="a9357-111">Las API de REST del servicio Búsqueda de Azure están documentadas en [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9357-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="a9357-112">En los siguientes pasos, podrá crear un índice, cargar documentos, consultar el índice y, a continuación, consultar el sistema en busca de información de servicio.</span><span class="sxs-lookup"><span data-stu-id="a9357-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="a9357-113">Para completar estos pasos, necesitará un servicio Búsqueda de Azure y `api-key`.</span><span class="sxs-lookup"><span data-stu-id="a9357-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="a9357-114">Consulte [Crear un servicio Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener instrucciones sobre cómo empezar.</span><span class="sxs-lookup"><span data-stu-id="a9357-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="a9357-115">Creación de un índice</span><span class="sxs-lookup"><span data-stu-id="a9357-115">Create an index</span></span>
1. <span data-ttu-id="a9357-116">Inicie Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a9357-116">Start Fiddler.</span></span> <span data-ttu-id="a9357-117">En el menú **Archivo**, desactive **Capturar tráfico** para ocultar la actividad HTTP irrelevante que no está relacionada con la tarea actual.</span><span class="sxs-lookup"><span data-stu-id="a9357-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="a9357-118">En la pestaña **Compositor** , formulará una solicitud similar a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="a9357-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="a9357-119">Seleccione **PUT**.</span><span class="sxs-lookup"><span data-stu-id="a9357-119">Select **PUT**.</span></span>
4. <span data-ttu-id="a9357-120">Escriba una dirección URL que especifica la dirección URL del servicio, los atributos de la solicitud y la versión de la API.</span><span class="sxs-lookup"><span data-stu-id="a9357-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="a9357-121">Algunos indicadores que tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="a9357-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="a9357-122">Use HTTPS como el prefijo.</span><span class="sxs-lookup"><span data-stu-id="a9357-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="a9357-123">El atributo de solicitud es "/índices/hoteles".</span><span class="sxs-lookup"><span data-stu-id="a9357-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="a9357-124">Esto le indica a la búsqueda que cree un índice llamado "hoteles".</span><span class="sxs-lookup"><span data-stu-id="a9357-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="a9357-125">La versión de la API se escribe en minúsculas y se especifica como "?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="a9357-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="a9357-126">Las versiones de API son importantes porque Búsqueda de Azure implementa actualizaciones regularmente.</span><span class="sxs-lookup"><span data-stu-id="a9357-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="a9357-127">En raras ocasiones, una actualización de servicio puede presentar un cambio innovador en la API.</span><span class="sxs-lookup"><span data-stu-id="a9357-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="a9357-128">Por este motivo, Búsqueda de Azure requiere una versión de la API en cada solicitud para que tenga el control total sobre cuál se usa.</span><span class="sxs-lookup"><span data-stu-id="a9357-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="a9357-129">La URL completa debe ser similar al siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9357-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="a9357-130">Especifique el encabezado de la solicitud al reemplazar el host y la clave de API por valores que son válidos para su servicio.</span><span class="sxs-lookup"><span data-stu-id="a9357-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="a9357-131">En el cuerpo de la solicitud, pegue los campos que componen la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="a9357-131">In Request Body, paste in the fields that make up the index definition.</span></span>

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
7. <span data-ttu-id="a9357-132">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a9357-132">Click **Execute**.</span></span>

<span data-ttu-id="a9357-133">En unos segundos verá una respuesta HTTP 201 en la lista de sesiones, que indica que el índice se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9357-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="a9357-134">Si obtiene HTTP 504, compruebe que la URL especifique HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a9357-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="a9357-135">Si se muestra el error HTTP 400 o 404, compruebe el cuerpo de la solicitud para verificar que no haya errores al copiar/pegar.</span><span class="sxs-lookup"><span data-stu-id="a9357-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="a9357-136">Un HTTP 403 indica normalmente que hay un problema con la clave de API (es una clave no válida o un problema de sintaxis sobre cómo se específica la clave de API).</span><span class="sxs-lookup"><span data-stu-id="a9357-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="a9357-137">Carga de documentos</span><span class="sxs-lookup"><span data-stu-id="a9357-137">Load documents</span></span>
<span data-ttu-id="a9357-138">En la pestaña **Compositor** , se verá su solicitud para enviar documentos como a continuación.</span><span class="sxs-lookup"><span data-stu-id="a9357-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="a9357-139">El cuerpo de la solicitud contiene los datos de búsqueda de cuatro hoteles.</span><span class="sxs-lookup"><span data-stu-id="a9357-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="a9357-140">Seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="a9357-140">Select **POST**.</span></span>
2. <span data-ttu-id="a9357-141">Escriba una URL que comience con HTTPS, seguida de la URL del servicio y, después, "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="a9357-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="a9357-142">La URL completa debe ser similar al siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9357-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="a9357-143">El encabezado de la solicitud debe ser igual que antes.</span><span class="sxs-lookup"><span data-stu-id="a9357-143">Request Header should be the same as before.</span></span> <span data-ttu-id="a9357-144">Recuerde que reemplazó el host y la clave de API con valores que son válidos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a9357-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="a9357-145">El cuerpo de la solicitud contiene cuatro documentos que se van agregar al índice de hoteles.</span><span class="sxs-lookup"><span data-stu-id="a9357-145">The Request Body contains four documents to be added to the hotels index.</span></span>

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
             "description": "This could be the one",
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
5. <span data-ttu-id="a9357-146">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a9357-146">Click **Execute**.</span></span>

<span data-ttu-id="a9357-147">En unos pocos segundos debe ver una respuesta HTTP 200 en la lista de sesiones.</span><span class="sxs-lookup"><span data-stu-id="a9357-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="a9357-148">Esto indica que los documentos se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9357-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="a9357-149">Si obtiene un 207, al menos un documento no pudo cargarse.</span><span class="sxs-lookup"><span data-stu-id="a9357-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="a9357-150">Si obtiene un error 404, se ha producido un error de sintaxis en el encabezado o en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a9357-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="a9357-151">Consultas al índice</span><span class="sxs-lookup"><span data-stu-id="a9357-151">Query the index</span></span>
<span data-ttu-id="a9357-152">Ahora que se han cargado el índice y los documentos, puede emitir consultas con ellos.</span><span class="sxs-lookup"><span data-stu-id="a9357-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="a9357-153">En la pestaña **Compositor**, el comando **GET** que consulta su servicio será similar a la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a9357-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="a9357-154">Seleccione **GET**.</span><span class="sxs-lookup"><span data-stu-id="a9357-154">Select **GET**.</span></span>
2. <span data-ttu-id="a9357-155">Escriba una URL que comience por HTTPS, seguida de la URL del servicio, después "/indexes/<'indexname'>/docs?" y, después, los parámetros de la consulta.</span><span class="sxs-lookup"><span data-stu-id="a9357-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="a9357-156">A modo de ejemplo, use la siguiente URL, que reemplaza el nombre del host de ejemplo por uno que es válido para su servicio.</span><span class="sxs-lookup"><span data-stu-id="a9357-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="a9357-157">Esta consulta busca el término “motel” y recupera las categorías de faceta para las calificaciones.</span><span class="sxs-lookup"><span data-stu-id="a9357-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="a9357-158">El encabezado de la solicitud debe ser igual que antes.</span><span class="sxs-lookup"><span data-stu-id="a9357-158">Request Header should be the same as before.</span></span> <span data-ttu-id="a9357-159">Recuerde que reemplazó el host y la clave de API con valores que son válidos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="a9357-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="a9357-160">El código de respuesta debe ser 200 y el resultado de la respuesta debe ser similar a la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a9357-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="a9357-161">La siguiente consulta de ejemplo proviene del tema [Operación de índice de búsqueda (API de Búsqueda de Azure)](http://msdn.microsoft.com/library/dn798927.aspx) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="a9357-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="a9357-162">Muchas de las consultas de ejemplo en este tema incluyen espacios, que no están permitidos en Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a9357-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="a9357-163">Reemplace cada espacio por un carácter + antes de pegar la cadena de la consulta e intentar la consulta en Fiddler:</span><span class="sxs-lookup"><span data-stu-id="a9357-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="a9357-164">**Los espacios anteriores se reemplazan:**</span><span class="sxs-lookup"><span data-stu-id="a9357-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="a9357-165">**Los espacios posteriores se reemplazan por +:**</span><span class="sxs-lookup"><span data-stu-id="a9357-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="a9357-166">Consultas al sistema</span><span class="sxs-lookup"><span data-stu-id="a9357-166">Query the system</span></span>
<span data-ttu-id="a9357-167">También puede consultar al sistema para obtener recuentos de documentos y consumo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a9357-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="a9357-168">En la pestaña **Compositor** , su solicitud será similar a la siguiente y la respuesta devolverá un recuento de la cantidad de documentos y el espacio usado.</span><span class="sxs-lookup"><span data-stu-id="a9357-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="a9357-169">Seleccione **GET**.</span><span class="sxs-lookup"><span data-stu-id="a9357-169">Select **GET**.</span></span>
2. <span data-ttu-id="a9357-170">Escriba una URL que incluya la URL de su servicio, seguida de "/indexes/hotels/stats?api-version=2016-09-01":</span><span class="sxs-lookup"><span data-stu-id="a9357-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="a9357-171">Especifique el encabezado de la solicitud al reemplazar el host y la clave de API por valores que son válidos para su servicio.</span><span class="sxs-lookup"><span data-stu-id="a9357-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="a9357-172">Deje vacío el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a9357-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="a9357-173">Haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a9357-173">Click **Execute**.</span></span> <span data-ttu-id="a9357-174">Debe ver un código de estado HTTP 200 en la lista de sesiones.</span><span class="sxs-lookup"><span data-stu-id="a9357-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="a9357-175">Seleccione la entrada enviada para su comando.</span><span class="sxs-lookup"><span data-stu-id="a9357-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="a9357-176">Haga clic en la pestaña **Inspectores**, en **Encabezados** y seleccione el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a9357-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="a9357-177">Debe ver el recuento de documentos y el tamaño del almacenamiento (en KB).</span><span class="sxs-lookup"><span data-stu-id="a9357-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9357-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9357-178">Next steps</span></span>
<span data-ttu-id="a9357-179">Consulte [Administración del servicio de búsqueda en Microsoft Azure](search-manage.md) para un enfoque sin código para administrar y usar Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9357-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
