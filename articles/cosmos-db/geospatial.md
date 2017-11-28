---
title: Trabajo con datos geoespaciales en Azure Cosmos DB | Microsoft Docs
description: "Comprenda cómo crear, indexar y consultar objetos espaciales con Azure Cosmos DB y la API de DocumentDB."
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="c8cc2-103">Trabajo con datos geoespaciales de ubicación y de GeoJSON en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8cc2-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="c8cc2-104">Este artículo es una introducción a la funcionalidad geoespacial en [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="c8cc2-105">Después de leer este artículo, podrá responder a las preguntas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c8cc2-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="c8cc2-106">¿Cómo almaceno los datos espaciales en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c8cc2-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="c8cc2-107">¿Cómo puedo consultar los datos geoespaciales en Azure Cosmos DB en SQL y LINQ?</span><span class="sxs-lookup"><span data-stu-id="c8cc2-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="c8cc2-108">¿Qué tengo que hacer para habilitar y deshabilitar la indexación en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c8cc2-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="c8cc2-109">Este artículo muestra cómo trabajar con datos espaciales con la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="c8cc2-110">Consulte este [proyecto de GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para obtener ejemplos de código.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="c8cc2-111">Introducción a los datos espaciales</span><span class="sxs-lookup"><span data-stu-id="c8cc2-111">Introduction to spatial data</span></span>
<span data-ttu-id="c8cc2-112">Los datos espaciales describen la posición y la forma de los objetos en el espacio.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="c8cc2-113">En la mayoría de las aplicaciones, estos se refieren a objetos situados la tierra, y son por ello datos geoespaciales.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="c8cc2-114">Los datos espaciales pueden usarse para representar la ubicación de una persona, un lugar de interés o el límite de una ciudad o un lago.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="c8cc2-115">Casos de uso más comunes suelen implicar las consultas de búsqueda por proximidad, por ejemplo, "encontrar todas las cafeterías cerca de la ubicación actual".</span><span class="sxs-lookup"><span data-stu-id="c8cc2-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="c8cc2-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="c8cc2-116">GeoJSON</span></span>
<span data-ttu-id="c8cc2-117">Azure Cosmos DB admite la indexación y consulta de datos de puntos geoespaciales que se representan mediante la [especificación GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="c8cc2-118">Las estructuras de datos de GeoJSON son siempre objetos JSON válidos, por lo que se pueden almacenar y consultar mediante Azure Cosmos DB sin tener que usar herramientas ni bibliotecas especializadas.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="c8cc2-119">El SDK de Azure Cosmos DB proporcionan clases y métodos auxiliares que facilitan el trabajo con datos espaciales.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="c8cc2-120">Elementos Point, LineString y Polygon</span><span class="sxs-lookup"><span data-stu-id="c8cc2-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="c8cc2-121">Un **punto** denota una posición única en el espacio.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="c8cc2-122">En los datos geoespaciales, un elemento Point (punto) representa la ubicación exacta, que puede ser una dirección de una tienda de ultramarinos, un quiosco, un automóvil o una ciudad.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="c8cc2-123">Un punto se representa en GeoJSON (y Azure Cosmos DB) mediante su par de coordenadas o su longitud y latitud.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="c8cc2-124">Este es un ejemplo JSON para un punto.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="c8cc2-125">**Puntos en Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="c8cc2-126">La especificación de GeoJSON especifica primero la longitud y segundo la latitud.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="c8cc2-127">Al igual que en otras aplicaciones de mapeado, la longitud y la latitud son ángulos y se representan en grados.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="c8cc2-128">Los valores de longitud se miden a partir del meridiano cero y están comprendidos entre -180 y 180.0 grados, mientras que los valores de latitud se miden a partir del Ecuador y están comprendidos entre -90,0 y 90,0 grados.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="c8cc2-129">Azure Cosmos DB interpreta las coordenadas tal como están representadas por el sistema de referencia WGS-84.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="c8cc2-130">Consulte a continuación para obtener más detalles acerca de los sistemas de coordenadas de referencia.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="c8cc2-131">Esto se puede insertar en un documento Azure Cosmos DB tal como se muestra en este ejemplo de un perfil de usuario que contiene datos de ubicación:</span><span class="sxs-lookup"><span data-stu-id="c8cc2-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="c8cc2-132">**Uso de perfil con una ubicación almacenada en Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="c8cc2-133">Además de los puntos, GeoJSON también admite LineStrings y polígonos.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="c8cc2-134">**LineStrings** representan una serie de dos o más puntos en el espacio y los segmentos que los conectan.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="c8cc2-135">En los datos geoespaciales, los elementos LineString se usan normalmente para representar autopistas o ríos.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="c8cc2-136">Un elemento **Polygon** (polígono) es un área delimitada por puntos conectados que forman un elemento LineString cerrado.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="c8cc2-137">Los polígonos se usan normalmente para representar formaciones naturales como lagos, o jurisdicciones políticas como estados y ciudades.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="c8cc2-138">Este es un ejemplo de un Polygon en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="c8cc2-139">**Polygons en GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="c8cc2-140">La especificación de GeoJSON requiere que para que un elemento Polygon sea válido, el último par de coordenadas indicado tiene que ser el mismo que el primero, para así crear una forma cerrada.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="c8cc2-141">El orden de los puntos dentro de un elemento Polygon debe especificarse siguiendo el sentido contrario al de las agujas del reloj.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="c8cc2-142">Un elemento Polygon cuyos puntos se hayan especificado en el sentido de las agujas del reloj representa el inverso de la región dentro de él.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="c8cc2-143">Además de puntos, LineStrings y polígonos, GeoJSON también especifica la representación de cómo agrupar varias ubicaciones geoespaciales, así como la forma de asociar propiedades arbitrarias a la ubicación geográfica como un **Característica**.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="c8cc2-144">Dado que estos objetos son JSON válidos, se pueden almacenar y procesar todos en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="c8cc2-145">Sin embargo, Azure Cosmos DB solo admite la indexación automática de puntos.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="c8cc2-146">Sistemas de coordenadas de referencia</span><span class="sxs-lookup"><span data-stu-id="c8cc2-146">Coordinate reference systems</span></span>
<span data-ttu-id="c8cc2-147">Dado que la forma de la tierra es irregular, las coordenadas de los datos geoespaciales se representa en muchos sistemas de coordenadas de referencia (CRS), cada uno con sus propios marcos de referencia y unidades de medida.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="c8cc2-148">Por ejemplo, la "National Grid of Britain" es un sistema de referencia muy preciso para el Reino Unido, pero no fuera de él.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="c8cc2-149">El sistema de coordenadas de referencia más popular en uso hoy en día es el Sistema Geodésico Mundial [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="c8cc2-150">Los dispositivos GPS y muchos servicios de mapeado como Google Maps y API de Bing Maps, usan WGS 84.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="c8cc2-151">Azure Cosmos DB admite indexación y consulta de datos geoespaciales usando solo el sistema de coordenadas WGS 84.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="c8cc2-152">Creación de documentos con datos espaciales</span><span class="sxs-lookup"><span data-stu-id="c8cc2-152">Creating documents with spatial data</span></span>
<span data-ttu-id="c8cc2-153">Al crear documentos que contengan valores GeoJSON, se indizan automáticamente con un índice espacial de acuerdo con la directiva de indexación de la colección.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="c8cc2-154">Si está trabajando con un SDK de Azure Cosmos DB en un lenguaje de tipo dinámico como Python o Node.js, debe crear especificaciones GeoJSON válidas.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="c8cc2-155">**Creación de documentos con datos geoespaciales en Node.js**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="c8cc2-156">Si está trabajando con API de DocumentDB, puede usar las clases `Point` y `Polygon` en el espacio de nombres `Microsoft.Azure.Documents.Spatial` para insertar información de ubicación dentro de los objetos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="c8cc2-157">Estas clases ayudan a simplificar la serialización y deserialización de datos espaciales en GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="c8cc2-158">**Creación de documentos con datos geoespaciales en .NET**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="c8cc2-159">Si no dispone de la información de latitud y longitud, pero tiene los nombres de ubicación como ciudad o país o direcciones físicas, puede buscar las coordenadas reales mediante un servicio de codificación geográfica como servicios de REST de Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="c8cc2-160">Obtener más información acerca de la codificación geográfica de Bing Maps [aquí](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="c8cc2-161">Consulta de tipos espaciales</span><span class="sxs-lookup"><span data-stu-id="c8cc2-161">Querying spatial types</span></span>
<span data-ttu-id="c8cc2-162">Ahora que ya hemos visto cómo insertar datos geoespaciales, echemos un vistazo a cómo consultar estos datos mediante Azure Cosmos DB con SQL y LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="c8cc2-163">Funciones integradas SQL espaciales</span><span class="sxs-lookup"><span data-stu-id="c8cc2-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="c8cc2-164">Azure Cosmos DB admite las siguientes funciones integradas de Open Geospatial Consortium (OGC) para realizar consultas geoespaciales.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="c8cc2-165">Para obtener más detalles sobre el conjunto completo de funciones integradas en el lenguaje SQL, vea [Consultas de Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="c8cc2-166"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="c8cc2-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="c8cc2-167"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="c8cc2-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8cc2-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c8cc2-169">Devuelve la distancia entre dos expresiones Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8cc2-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c8cc2-171">Devuelve una expresión booleana que indica si el primer objeto de GeoJSON (Point, Polygon o LineString) está en el segundo objeto de GeoJSON (Point, Polygon o LineString).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8cc2-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c8cc2-173">Devuelve una expresión booleana que indica si los dos objetos de GeoJSON especificados (Point, Polygon o LineString) intersecan.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8cc2-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="c8cc2-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="c8cc2-175">Devuelve un valor booleano que indica si la expresión de Point, Polygon o LineString de GeoJSON especificada es válida.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8cc2-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="c8cc2-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="c8cc2-177">Devuelve un valor JSON que contiene un valor booleano si la expresión de Point, Polygon o LineString de GeoJSON especificada es válida; si no es válida, devuelve también el motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="c8cc2-178">Las funciones espaciales pueden usarse para realizar consultas de proximidad con datos espaciales.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="c8cc2-179">Por ejemplo, aquí hay una consulta que devuelve todos los documentos de la familia que estén dentro de un radio de 30 km de la ubicación especificada mediante la función integrada ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="c8cc2-180">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="c8cc2-181">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="c8cc2-182">Si incluye la indexación espacial en la directiva de indexación, las "consultas de distancia" se atenderán eficazmente a través del índice.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="c8cc2-183">Para obtener más detalles sobre la indexación espacial, consulte la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="c8cc2-184">Aunque no tenga un índice espacial para las rutas de acceso especificadas, aún podrá realizar consultas espaciales mediante la especificación del encabezado de solicitud `x-ms-documentdb-query-enable-scan` con el valor establecido en "true".</span><span class="sxs-lookup"><span data-stu-id="c8cc2-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="c8cc2-185">En. NET, para hacerlo es preciso pasar el argumento **FeedOptions** opcional en consultas en las que [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) está establecido en true.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="c8cc2-186">ST_WITHIN puede usarse para comprobar si un punto se encuentra dentro de un elemento Polygon.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="c8cc2-187">Normalmente, los elementos Polygon se usan para representar límites, como códigos postales, fronteras o formaciones naturales.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="c8cc2-188">Una vez más, si incluye la indexación espacial en la directiva de indexación, las consultas "interiores" se atenderán eficazmente a través del índice.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="c8cc2-189">Los argumentos de Polygon en ST_WITHIN solo pueden contener un anillo individual, es decir, los elementos Polygon no deben contener orificios.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="c8cc2-190">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="c8cc2-191">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="c8cc2-192">De forma parecida a cómo funcionan los tipos no coincidentes en una consulta de Azure Cosmos DB, si el valor de ubicación especificado en cualquier argumento está mal formado o no es válido, se evaluará como **sin definir** y el documento evaluado se omite de los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="c8cc2-193">Si la consulta no devuelve resultados, ejecute ST_ISVALIDDETAILED para depurarla y saber por qué el tipo espacial no es válido.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="c8cc2-194">Azure Cosmos DB también admite la realización de consultas inversas, es decir, puede indexar elementos Polygon o líneas en Azure Cosmos DB y, luego, consultar las áreas que contienen un punto especificado.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="c8cc2-195">Este patrón se utiliza habitualmente en logística para identificar, por ejemplo, cuando un camión entra o sale de un área designada.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="c8cc2-196">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="c8cc2-197">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="c8cc2-198">ST_ISVALID y ST_ISVALIDDETAILED pueden usarse para comprobar si un objeto espacial es válido.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="c8cc2-199">Por ejemplo, la consulta siguiente comprueba la validez de un punto con un valor de latitud fuera del intervalo (-132,8).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="c8cc2-200">ST_ISVALID devuelve solo un valor booleano y ST_ISVALIDDETAILED devuelve el valor booleano y una cadena que contiene el motivo por el que se considera no válida.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="c8cc2-201">** Consultar **</span><span class="sxs-lookup"><span data-stu-id="c8cc2-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="c8cc2-202">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="c8cc2-203">Estas funciones también se pueden usar para validar elementos Polygon.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="c8cc2-204">Por ejemplo, aquí usamos ST_ISVALIDDETAILED para validar un elemento Polygon que no está cerrado.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="c8cc2-205">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="c8cc2-206">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="c8cc2-207">Consultas LINQ en el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="c8cc2-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="c8cc2-208">El SDK de .NET de DocumentDB también proporciona métodos de código auxiliar `Distance()` y `Within()` para su uso dentro de las expresiones LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="c8cc2-209">El proveedor LINQ de DocumentDB traduce estas llamadas al método a las llamadas de función integrada de SQL equivalentes (ST_DISTANCE y ST_WITHIN respectivamente).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="c8cc2-210">Este es un ejemplo de una consulta LINQ que busca todos los documentos de la colección de Azure Cosmos DB cuyo valor de "ubicación" se encuentra en un radio de 30 km del punto especificado mediante LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="c8cc2-211">**Consulta LINQ de distancia**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="c8cc2-212">De forma similar, aquí vemos una consulta para buscar todos los documentos cuya "ubicación" está dentro del cuadro o del elemento Polygon especificado.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="c8cc2-213">**Consulta LINQ interna**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="c8cc2-214">Ahora que hemos visto cómo consultar documentos con LINQ y SQL, echemos un vistazo a cómo configurar Azure Cosmos DB para la indexación espacial.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="c8cc2-215">Indización</span><span class="sxs-lookup"><span data-stu-id="c8cc2-215">Indexing</span></span>
<span data-ttu-id="c8cc2-216">Como se describe en el artículo [Indexación independiente de esquemas con Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf), diseñamos el motor de base de datos de Azure Cosmos DB para que sea realmente independiente de los esquemas y proporcione compatibilidad de primera clase con JSON.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="c8cc2-217">Ahora el motor de base de datos de escritura optimizado de Azure Cosmos DB también entiende de forma nativa los datos espaciales (puntos, elementos Polygon y líneas) representados en el estándar GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="c8cc2-218">En pocas palabras, la geometría se proyecta a partir de coordenadas geodésicas en un plano 2D; después, se divide progresivamente en celdas con un **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="c8cc2-219">Estas celdas se asignan a 1D según la ubicación de la celda dentro de una **curva de Hilbert**, que conserva la localidad de los puntos.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="c8cc2-220">Además, al indexar los datos de ubicación, estos pasan por un proceso conocido como **teselación**, es decir, todas las celdas que se cruzan en una ubicación se identifican y se almacenan como claves en el índice de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="c8cc2-221">En el momento de la consulta, los argumentos como puntos y elementos Polygon también se teselan para extraer los intervalos de Id. de celda pertinentes, y luego se usan para recuperar los datos del índice.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="c8cc2-222">Si especifica una directiva de indexación que incluye el índice espacial para / * (todas las rutas de acceso), entonces todos los puntos dentro de la colección se indexan para que las consultas espaciales resulten eficaces (ST_WITHIN y ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="c8cc2-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="c8cc2-223">Los índices espaciales no tienen un valor de precisión y usan siempre un valor de precisión predeterminado.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="c8cc2-224">Azure Cosmos DB admite la indexación automática de puntos, elementos Polygon y LineString.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="c8cc2-225">El siguiente fragmento JSON, muestra una directiva de indexación con la indexación espacial habilitada, es decir, indexar cualquier punto GeoJSON que se encuentre dentro de los documentos para la consulta espacial.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="c8cc2-226">Si va a modificar la directiva de indexación mediante el Portal de Azure, puede especificar el siguiente JSON para que la directiva de indexación habilite la indexación espacial en la colección.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="c8cc2-227">**JSON de directiva de indexación de una colección con la característica espacial habilitada para puntos y elementos Polygon**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="c8cc2-228">Aquí vemos un fragmento de código de .NET que muestra cómo crear una colección con índices espaciales activados para todas las rutas que contengan puntos.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="c8cc2-229">**Creación de una colección con indexación espacial**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="c8cc2-230">Y aquí vemos cómo puede modificar una colección existente para aprovechar las ventajas de la indexación espacial de los puntos que se almacenan en los documentos.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="c8cc2-231">**Modificación de una colección ya existente con indexación espacial**</span><span class="sxs-lookup"><span data-stu-id="c8cc2-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="c8cc2-232">Si el valor GeoJSON de la ubicación que se encuentra en el documento es incorrecto o no válido, no se indexará para realizar consultas espaciales.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="c8cc2-233">Puede validar los valores de ubicación mediante ST_ISVALID y ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="c8cc2-234">Si la definición de la colección incluye una clave de partición, no se notifica el progreso de transformación de la indexación.</span><span class="sxs-lookup"><span data-stu-id="c8cc2-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c8cc2-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8cc2-235">Next steps</span></span>
<span data-ttu-id="c8cc2-236">Ahora que ya sabe cómo empezar a trabajar con la compatibilidad geoespacial en Azure Cosmos DB, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8cc2-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="c8cc2-237">Comenzar a codificar con los [ejemplos de código geoespacial .NET en GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="c8cc2-238">Empezar a realizar consultas geoespaciales en el [Área de consultas de Azure Cosmos DB](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="c8cc2-239">Obtener más información sobre [Consultar Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="c8cc2-240">Obtener más información sobre [Directivas de indexación de Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="c8cc2-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

