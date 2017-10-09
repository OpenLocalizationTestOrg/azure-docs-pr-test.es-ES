---
title: aaaWorking con datos geoespaciales en la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Comprender cómo toocreate, indizar y consultar objetos espaciales con base de datos de Azure Cosmos y Hola API de documentos."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="17275-103">Trabajo con datos geoespaciales de ubicación y de GeoJSON en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="17275-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="17275-104">En este artículo es una introducción toohello geospatial la funcionalidad de [base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="17275-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="17275-105">Después de leerla, será hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="17275-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="17275-106">¿Cómo almaceno los datos espaciales en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="17275-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="17275-107">¿Cómo puedo consultar los datos geoespaciales en Azure Cosmos DB en SQL y LINQ?</span><span class="sxs-lookup"><span data-stu-id="17275-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="17275-108">¿Qué tengo que hacer para habilitar y deshabilitar la indexación en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="17275-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="17275-109">Este artículo muestra cómo toowork con datos espaciales con Hola API de documentos.</span><span class="sxs-lookup"><span data-stu-id="17275-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="17275-110">Consulte este [proyecto de GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para obtener ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="17275-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="17275-111">Introducción toospatial data</span><span class="sxs-lookup"><span data-stu-id="17275-111">Introduction toospatial data</span></span>
<span data-ttu-id="17275-112">Datos espaciales describen la posición de Hola y la forma de objetos en el espacio.</span><span class="sxs-lookup"><span data-stu-id="17275-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="17275-113">En la mayoría de las aplicaciones, estos corresponden tooobjects tierra de hello, es decir, datos geoespaciales.</span><span class="sxs-lookup"><span data-stu-id="17275-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="17275-114">Datos espaciales pueden ser utilizados toorepresent Hola la ubicación de una persona, un lugar de interés o límite de Hola de una ciudad o un lago.</span><span class="sxs-lookup"><span data-stu-id="17275-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="17275-115">Casos de uso más comunes suelen implicar las consultas de búsqueda por proximidad, por ejemplo, "encontrar todas las cafeterías cerca de la ubicación actual".</span><span class="sxs-lookup"><span data-stu-id="17275-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="17275-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="17275-116">GeoJSON</span></span>
<span data-ttu-id="17275-117">Base de datos de Azure Cosmos admite indización y consulta de geospatial punto de datos que se representa con hello [GeoJSON especificación](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="17275-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="17275-118">Las estructuras de datos de GeoJSON son siempre objetos JSON válidos, por lo que se pueden almacenar y consultar mediante Azure Cosmos DB sin tener que usar herramientas ni bibliotecas especializadas.</span><span class="sxs-lookup"><span data-stu-id="17275-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="17275-119">Hello Azure Cosmos DB SDK proporciona clases auxiliares y métodos que hacen que sea fácil toowork con datos espaciales.</span><span class="sxs-lookup"><span data-stu-id="17275-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="17275-120">Elementos Point, LineString y Polygon</span><span class="sxs-lookup"><span data-stu-id="17275-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="17275-121">Un **punto** denota una posición única en el espacio.</span><span class="sxs-lookup"><span data-stu-id="17275-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="17275-122">En datos geoespaciales, un punto representa la ubicación exacta de hello, que podría ser una dirección postal de una tienda de comestibles, un quiosco, un automóvil o una ciudad.</span><span class="sxs-lookup"><span data-stu-id="17275-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="17275-123">Un punto se representa en GeoJSON (y Azure Cosmos DB) mediante su par de coordenadas o su longitud y latitud.</span><span class="sxs-lookup"><span data-stu-id="17275-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="17275-124">Este es un ejemplo JSON para un punto.</span><span class="sxs-lookup"><span data-stu-id="17275-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="17275-125">**Puntos en Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="17275-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="17275-126">Hola GeoJSON especificación especifica longitud primero y latitud segundo.</span><span class="sxs-lookup"><span data-stu-id="17275-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="17275-127">Al igual que en otras aplicaciones de mapeado, la longitud y la latitud son ángulos y se representan en grados.</span><span class="sxs-lookup"><span data-stu-id="17275-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="17275-128">Valores de longitud se miden desde Hola meridiano y están comprendidos entre -180 y 180.0 grados y la latitud valores se mide desde el ecuador de Hola y que existen entre-90.0 y 90.0 grados.</span><span class="sxs-lookup"><span data-stu-id="17275-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="17275-129">Base de datos de Azure Cosmos interpreta coordenadas tal como está representado por el sistema de referencia de hello WGS 84.</span><span class="sxs-lookup"><span data-stu-id="17275-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="17275-130">Consulte a continuación para obtener más detalles acerca de los sistemas de coordenadas de referencia.</span><span class="sxs-lookup"><span data-stu-id="17275-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="17275-131">Esto se puede insertar en un documento Azure Cosmos DB tal como se muestra en este ejemplo de un perfil de usuario que contiene datos de ubicación:</span><span class="sxs-lookup"><span data-stu-id="17275-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="17275-132">**Uso de perfil con una ubicación almacenada en Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="17275-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

<span data-ttu-id="17275-133">Además, toopoints, GeoJSON también admite LineStrings y polígonos.</span><span class="sxs-lookup"><span data-stu-id="17275-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="17275-134">**LineStrings** representan una serie de dos o más puntos en el espacio y Hola segmentos de línea que conectan.</span><span class="sxs-lookup"><span data-stu-id="17275-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="17275-135">En los datos geoespaciales, LineStrings son utilizadas toorepresent autopistas o ríos.</span><span class="sxs-lookup"><span data-stu-id="17275-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="17275-136">Un elemento **Polygon** (polígono) es un área delimitada por puntos conectados que forman un elemento LineString cerrado.</span><span class="sxs-lookup"><span data-stu-id="17275-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="17275-137">Polígonos son utilizadas toorepresent formaciones natural como lagos o políticos jurisdicciones como Estados y ciudades.</span><span class="sxs-lookup"><span data-stu-id="17275-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="17275-138">Este es un ejemplo de un Polygon en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17275-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="17275-139">**Polygons en GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="17275-139">**Polygons in GeoJSON**</span></span>

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> <span data-ttu-id="17275-140">Hola GeoJSON especificación requiere que para los polígonos válidos, hello último par de coordenadas proporcionada debe ser igual Hola como hello en primer lugar, toocreate una forma cerrada.</span><span class="sxs-lookup"><span data-stu-id="17275-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="17275-141">El orden de los puntos dentro de un elemento Polygon debe especificarse siguiendo el sentido contrario al de las agujas del reloj.</span><span class="sxs-lookup"><span data-stu-id="17275-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="17275-142">Un polígono especificado en el orden de las agujas del reloj representa inverso de Hola de región de hello dentro de él.</span><span class="sxs-lookup"><span data-stu-id="17275-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="17275-143">En suma tooPoint, LineString y del polígono, GeoJSON también especifica representación Hola para saber cómo toogroup varias ubicaciones geoespaciales, así como la tooassociate propiedades arbitrarias con ubicación geográfica como una **característica**.</span><span class="sxs-lookup"><span data-stu-id="17275-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="17275-144">Dado que estos objetos son JSON válidos, se pueden almacenar y procesar todos en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17275-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="17275-145">Sin embargo, Azure Cosmos DB solo admite la indexación automática de puntos.</span><span class="sxs-lookup"><span data-stu-id="17275-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="17275-146">Sistemas de coordenadas de referencia</span><span class="sxs-lookup"><span data-stu-id="17275-146">Coordinate reference systems</span></span>
<span data-ttu-id="17275-147">Puesto que forma Hola de tierra de hello es irregular, coordenadas de datos geoespaciales se representa en muchos sistemas de coordenadas de referencia (CR), cada uno con sus propios marcos de referencia y las unidades de medida.</span><span class="sxs-lookup"><span data-stu-id="17275-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="17275-148">Por ejemplo, "Cuadrícula nacional de Bretaña" hello es un sistema de referencia es muy preciso para hello Reino Unido, pero no fuera de él.</span><span class="sxs-lookup"><span data-stu-id="17275-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="17275-149">Hello CRS más populares en uso hoy en día es hello del sistema geodésico mundial [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="17275-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="17275-150">Los dispositivos GPS y muchos servicios de mapeado como Google Maps y API de Bing Maps, usan WGS 84.</span><span class="sxs-lookup"><span data-stu-id="17275-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="17275-151">Base de datos de Azure Cosmos admite indización y consulta de datos geoespaciales mediante Hola WGS 84 CRS.</span><span class="sxs-lookup"><span data-stu-id="17275-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="17275-152">Creación de documentos con datos espaciales</span><span class="sxs-lookup"><span data-stu-id="17275-152">Creating documents with spatial data</span></span>
<span data-ttu-id="17275-153">Cuando haya creado los documentos que contienen valores de GeoJSON, se indizan automáticamente con un índice espacial en la directiva de indexación de acuerdo toohello de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="17275-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="17275-154">Si está trabajando con un SDK de Azure Cosmos DB en un lenguaje de tipo dinámico como Python o Node.js, debe crear especificaciones GeoJSON válidas.</span><span class="sxs-lookup"><span data-stu-id="17275-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="17275-155">**Creación de documentos con datos geoespaciales en Node.js**</span><span class="sxs-lookup"><span data-stu-id="17275-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

<span data-ttu-id="17275-156">Si está trabajando con hello DocumentDB APIs, puede usar hello `Point` y `Polygon` clases dentro de hello `Microsoft.Azure.Documents.Spatial` información de ubicación de espacio de nombres tooembed dentro de los objetos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17275-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="17275-157">Estas clases ayudan a simplificar Hola serialización y deserialización de datos espaciales en GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="17275-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="17275-158">**Creación de documentos con datos geoespaciales en .NET**</span><span class="sxs-lookup"><span data-stu-id="17275-158">**Create Document with Geospatial data in .NET**</span></span>

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

<span data-ttu-id="17275-159">Si no tiene información de latitud y longitud de hello, pero tiene direcciones físicas de Hola o nombre de la ubicación como la ciudad o el país, puede buscar coordenadas real hello mediante el uso de un servicio de codificación geográfica como servicios de REST de mapas de Bing.</span><span class="sxs-lookup"><span data-stu-id="17275-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="17275-160">Obtener más información acerca de la codificación geográfica de Bing Maps [aquí](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="17275-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="17275-161">Consulta de tipos espaciales</span><span class="sxs-lookup"><span data-stu-id="17275-161">Querying spatial types</span></span>
<span data-ttu-id="17275-162">Ahora que hemos llevado un vistazo a cómo los datos geoespaciales tooinsert, echemos un vistazo a cómo tooquery estos datos con la base de datos de Cosmos de Azure con SQL y LINQ.</span><span class="sxs-lookup"><span data-stu-id="17275-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="17275-163">Funciones integradas SQL espaciales</span><span class="sxs-lookup"><span data-stu-id="17275-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="17275-164">Base de datos de Azure Cosmos admite Hola siguiendo las funciones integradas de Open Geospatial Consortium (OGC) para realizar consultas geoespaciales.</span><span class="sxs-lookup"><span data-stu-id="17275-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="17275-165">Para obtener más detalles sobre el conjunto completo de Hola de funciones integradas en hello lenguaje SQL, consulte demasiado[base de datos de consulta Azure Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="17275-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="17275-166"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="17275-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="17275-167"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="17275-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="17275-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="17275-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="17275-169">Devuelve la distancia de hello entre expresiones de punto de GeoJSON, polígono o LineString Hola dos.</span><span class="sxs-lookup"><span data-stu-id="17275-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="17275-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="17275-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="17275-171">Devuelve una expresión booleana que indica si es Hola primer GeoJSON objeto (punto, polígono o LineString) dentro de hello segundo GeoJSON objeto (punto, polígono o LineString).</span><span class="sxs-lookup"><span data-stu-id="17275-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="17275-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="17275-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="17275-173">Devuelve una expresión booleana que indica si se intersecan Hola dos GeoJSON objetos especificados (punto, polígono o LineString).</span><span class="sxs-lookup"><span data-stu-id="17275-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="17275-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="17275-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="17275-175">Devuelve un valor booleano que indica si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida.</span><span class="sxs-lookup"><span data-stu-id="17275-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="17275-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="17275-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="17275-177">Devuelve un valor JSON que contiene un valor booleano si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida y si no es válido, además Hola motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="17275-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="17275-178">Funciones espaciales pueden ser consultas de proximidad de tooperform utilizadas en los datos espaciales.</span><span class="sxs-lookup"><span data-stu-id="17275-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="17275-179">Por ejemplo, aquí es una consulta que devuelve la que familia de todos los documentos que está dentro de 30 km de hello ubicación especificada mediante hello ST_DISTANCE función integrada.</span><span class="sxs-lookup"><span data-stu-id="17275-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="17275-180">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="17275-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="17275-181">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="17275-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="17275-182">Si incluye los índices espaciales en su directiva de indexación, a continuación, "consultas de distancia" se servirá eficazmente a través del índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="17275-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="17275-183">Para obtener más detalles sobre los índices espaciales, vea sección hello más adelante.</span><span class="sxs-lookup"><span data-stu-id="17275-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="17275-184">Si no tienes espaciales índice para hello especifica las rutas de acceso, todavía puede realizar consultas espaciales especificando `x-ms-documentdb-query-enable-scan` establecida en el encabezado de solicitud con el valor de hello demasiado "verdadero".</span><span class="sxs-lookup"><span data-stu-id="17275-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="17275-185">En. NET, esto puede hacerse por pasar Hola opcional **FeedOptions** tooqueries de argumento con [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) establecer tootrue.</span><span class="sxs-lookup"><span data-stu-id="17275-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="17275-186">ST_WITHIN puede ser usado toocheck si se encuentra un punto dentro de un polígono.</span><span class="sxs-lookup"><span data-stu-id="17275-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="17275-187">Normalmente polígonos son límites de toorepresent usado como códigos postales, los límites de estado o formaciones naturales.</span><span class="sxs-lookup"><span data-stu-id="17275-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="17275-188">Nuevo si incluye los índices espaciales en su directiva de indexación, a continuación, "en" consultas se servirá eficazmente a través del índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="17275-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="17275-189">Argumentos de polígono en ST_WITHIN pueden contener solo un anillo único, es decir, Hola polígonos no debe contener vulnerabilidades en ellos.</span><span class="sxs-lookup"><span data-stu-id="17275-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="17275-190">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="17275-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="17275-191">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="17275-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="17275-192">Tipos de error de coincidencia de toohow similares funciona en la consulta de base de datos de Azure Cosmos, si el valor de la ubicación de hello especificado en el argumento está bien formado o no válido, a continuación, se evaluará demasiado**indefinido** Hola evaluada documento toobe omitido de Hola resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="17275-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="17275-193">Si la consulta no devuelve ningún resultado, ejecute toodebug ST_ISVALIDDETAILED ¿por qué tipo de hello spatail no es válido.</span><span class="sxs-lookup"><span data-stu-id="17275-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="17275-194">Base de datos de Azure Cosmos también admite la realización de consultas inversas, es decir, es posible indizar polígonos o líneas de base de datos de Azure Cosmos y consultar las áreas de Hola que contenga un punto especificado.</span><span class="sxs-lookup"><span data-stu-id="17275-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="17275-195">Este patrón es más frecuente en logística tooidentify por ejemplo, cuando un camión entra o sale de un área designada.</span><span class="sxs-lookup"><span data-stu-id="17275-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="17275-196">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="17275-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="17275-197">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="17275-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="17275-198">ST_ISVALID y ST_ISVALIDDETAILED pueden ser utilizado toocheck si un objeto espacial es válido.</span><span class="sxs-lookup"><span data-stu-id="17275-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="17275-199">Por ejemplo, hello después consulta comprueba la validez de Hola de un punto con un valor fuera del intervalo latitud (-132.8).</span><span class="sxs-lookup"><span data-stu-id="17275-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="17275-200">ST_ISVALID devuelve un valor de tipo Boolean y Hola a ST_ISVALIDDETAILED devuelve un valor booleano y una cadena que contiene el motivo de hello ¿por qué se considera no válida.</span><span class="sxs-lookup"><span data-stu-id="17275-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="17275-201">** Consultar **</span><span class="sxs-lookup"><span data-stu-id="17275-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="17275-202">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="17275-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="17275-203">Estas funciones también pueden ser polígonos de toovalidate usado.</span><span class="sxs-lookup"><span data-stu-id="17275-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="17275-204">Por ejemplo, aquí usamos ST_ISVALIDDETAILED toovalidate un polígono que no está cerrado.</span><span class="sxs-lookup"><span data-stu-id="17275-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="17275-205">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="17275-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="17275-206">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="17275-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="17275-207">Realizar consultas LINQ en hello SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="17275-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="17275-208">Hola documentos .NET SDK también proveedores stub métodos `Distance()` y `Within()` para su uso dentro de las expresiones de LINQ.</span><span class="sxs-lookup"><span data-stu-id="17275-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="17275-209">proveedor de DocumentDB LINQ Hello traduce estas llamadas toohello equivalente SQL función integrada llamadas al método (ST_DISTANCE y ST_WITHIN respectivamente).</span><span class="sxs-lookup"><span data-stu-id="17275-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="17275-210">Este es un ejemplo de una consulta LINQ que busca todos los documentos en la colección de base de datos de Azure Cosmos Hola cuyo valor de "ubicación" está dentro de un radio de 30km de hello especificada punto mediante LINQ.</span><span class="sxs-lookup"><span data-stu-id="17275-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="17275-211">**Consulta LINQ de distancia**</span><span class="sxs-lookup"><span data-stu-id="17275-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="17275-212">De forma similar, esta es una consulta para buscar todos los documentos de hello cuyo "ubicación" está dentro de hello especificado cuadro o polígono.</span><span class="sxs-lookup"><span data-stu-id="17275-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="17275-213">**Consulta LINQ interna**</span><span class="sxs-lookup"><span data-stu-id="17275-213">**LINQ query for Within**</span></span>

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


<span data-ttu-id="17275-214">Ahora que hemos llevado un vistazo a cómo los documentos de tooquery mediante LINQ y SQL, echemos un vistazo a cómo tooconfigure base de datos de Azure Cosmos para los índices espaciales.</span><span class="sxs-lookup"><span data-stu-id="17275-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="17275-215">Indización</span><span class="sxs-lookup"><span data-stu-id="17275-215">Indexing</span></span>
<span data-ttu-id="17275-216">Tal y como se ha descrito en hello [esquema independiente de la indexación con base de datos de Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papel, diseñamos toobe de motor de base de datos de Azure Cosmos DB realmente independiente del esquema y proporcionar soporte de primera clase para JSON.</span><span class="sxs-lookup"><span data-stu-id="17275-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="17275-217">motor de base de datos de escritura optimizado Hola de base de datos de Azure Cosmos entiende los datos espaciales (puntos, líneas y polígonos) representados en estándar de GeoJSON Hola.</span><span class="sxs-lookup"><span data-stu-id="17275-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="17275-218">En pocas palabras, geometry Hola se proyecta desde geodésicos coordenadas en un plano 2D, a continuación, dividir celdas mediante progresivamente un **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="17275-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="17275-219">Estas celdas están asignadas too1D basadas en ubicación de Hola de celda Hola dentro de un **curva de rellenado de espacio Hilbert**, que conserva una localidad de puntos.</span><span class="sxs-lookup"><span data-stu-id="17275-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="17275-220">Además cuando se indizan los datos de ubicación, pasa por un proceso conocido como **teselación**, es decir, todas las celdas de Hola que forman una intersección una ubicación se identifican y se almacenan como claves de índice de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="17275-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="17275-221">En el momento de la consulta, argumentos como puntos y polígonos también están divididas en mosaicos tooextract Hola intervalos de identificadores de celda relevante, utilizan datos de tooretrieve del índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="17275-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="17275-222">Si especifica una directiva de indexación que incluye el índice espacial para / * (todas las rutas de acceso), a continuación, se indizan todos los puntos que se encuentra en la colección de Hola para consultas espaciales eficaces (ST_WITHIN y ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="17275-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="17275-223">Los índices espaciales no tienen un valor de precisión y usan siempre un valor de precisión predeterminado.</span><span class="sxs-lookup"><span data-stu-id="17275-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="17275-224">Azure Cosmos DB admite la indexación automática de puntos, elementos Polygon y LineString.</span><span class="sxs-lookup"><span data-stu-id="17275-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="17275-225">Hello siguiente fragmento JSON muestra una directiva de indexación con habilitada la indización espacial, es decir, cualquier punto de GeoJSON que se encuentra dentro de los documentos para realizar consultas espaciales de índice.</span><span class="sxs-lookup"><span data-stu-id="17275-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="17275-226">Si va a modificar Hola indización directiva mediante Hola Portal de Azure, puede especificar Hola después JSON para la indización de directiva tooenable espacial de indización en la colección.</span><span class="sxs-lookup"><span data-stu-id="17275-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="17275-227">**JSON de directiva de indexación de una colección con la característica espacial habilitada para puntos y elementos Polygon**</span><span class="sxs-lookup"><span data-stu-id="17275-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

<span data-ttu-id="17275-228">Este es un fragmento de código de .NET que muestra cómo toocreate una colección de los índices espaciales activado para todas las rutas de acceso que contiene puntos.</span><span class="sxs-lookup"><span data-stu-id="17275-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="17275-229">**Creación de una colección con indexación espacial**</span><span class="sxs-lookup"><span data-stu-id="17275-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="17275-230">Y aquí es cómo puede modificar una ventaja de tootake colección existente de índices espaciales sobre los puntos que se almacenan dentro de los documentos.</span><span class="sxs-lookup"><span data-stu-id="17275-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="17275-231">**Modificación de una colección ya existente con indexación espacial**</span><span class="sxs-lookup"><span data-stu-id="17275-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="17275-232">Si ubicación hello GeoJSON valor dentro del documento de hello es incorrecto o no es válido, a continuación, lo no obtener indizará para realizar consultas espaciales.</span><span class="sxs-lookup"><span data-stu-id="17275-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="17275-233">Puede validar los valores de ubicación mediante ST_ISVALID y ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="17275-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="17275-234">Si la definición de la colección incluye una clave de partición, no se notifica el progreso de transformación de la indexación.</span><span class="sxs-lookup"><span data-stu-id="17275-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="17275-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17275-235">Next steps</span></span>
<span data-ttu-id="17275-236">Ahora que ha aprender acerca de cómo tooget empezar con compatibilidad de geospatial en la base de datos de Azure Cosmos, puede:</span><span class="sxs-lookup"><span data-stu-id="17275-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="17275-237">Comenzar a codificar con hello [ejemplos de código de Geospatial .NET en GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="17275-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="17275-238">Obtener las manos en geospatial consultando al hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="17275-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="17275-239">Obtener más información sobre [Consultar Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="17275-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="17275-240">Obtener más información sobre [Directivas de indexación de Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="17275-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

