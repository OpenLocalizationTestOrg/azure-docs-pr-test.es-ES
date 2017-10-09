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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Trabajo con datos geoespaciales de ubicación y de GeoJSON en Azure Cosmos DB
En este artículo es una introducción toohello geospatial la funcionalidad de [base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Después de leerla, será hello tooanswer pueda siguientes preguntas:

* ¿Cómo almaceno los datos espaciales en Azure Cosmos DB?
* ¿Cómo puedo consultar los datos geoespaciales en Azure Cosmos DB en SQL y LINQ?
* ¿Qué tengo que hacer para habilitar y deshabilitar la indexación en Azure Cosmos DB?

Este artículo muestra cómo toowork con datos espaciales con Hola API de documentos. Consulte este [proyecto de GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para obtener ejemplos de código.

## <a name="introduction-toospatial-data"></a>Introducción toospatial data
Datos espaciales describen la posición de Hola y la forma de objetos en el espacio. En la mayoría de las aplicaciones, estos corresponden tooobjects tierra de hello, es decir, datos geoespaciales. Datos espaciales pueden ser utilizados toorepresent Hola la ubicación de una persona, un lugar de interés o límite de Hola de una ciudad o un lago. Casos de uso más comunes suelen implicar las consultas de búsqueda por proximidad, por ejemplo, "encontrar todas las cafeterías cerca de la ubicación actual". 

### <a name="geojson"></a>GeoJSON
Base de datos de Azure Cosmos admite indización y consulta de geospatial punto de datos que se representa con hello [GeoJSON especificación](https://tools.ietf.org/html/rfc7946). Las estructuras de datos de GeoJSON son siempre objetos JSON válidos, por lo que se pueden almacenar y consultar mediante Azure Cosmos DB sin tener que usar herramientas ni bibliotecas especializadas. Hello Azure Cosmos DB SDK proporciona clases auxiliares y métodos que hacen que sea fácil toowork con datos espaciales. 

### <a name="points-linestrings-and-polygons"></a>Elementos Point, LineString y Polygon
Un **punto** denota una posición única en el espacio. En datos geoespaciales, un punto representa la ubicación exacta de hello, que podría ser una dirección postal de una tienda de comestibles, un quiosco, un automóvil o una ciudad.  Un punto se representa en GeoJSON (y Azure Cosmos DB) mediante su par de coordenadas o su longitud y latitud. Este es un ejemplo JSON para un punto.

**Puntos en Azure Cosmos DB**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Hola GeoJSON especificación especifica longitud primero y latitud segundo. Al igual que en otras aplicaciones de mapeado, la longitud y la latitud son ángulos y se representan en grados. Valores de longitud se miden desde Hola meridiano y están comprendidos entre -180 y 180.0 grados y la latitud valores se mide desde el ecuador de Hola y que existen entre-90.0 y 90.0 grados. 
> 
> Base de datos de Azure Cosmos interpreta coordenadas tal como está representado por el sistema de referencia de hello WGS 84. Consulte a continuación para obtener más detalles acerca de los sistemas de coordenadas de referencia.
> 
> 

Esto se puede insertar en un documento Azure Cosmos DB tal como se muestra en este ejemplo de un perfil de usuario que contiene datos de ubicación:

**Uso de perfil con una ubicación almacenada en Azure Cosmos DB**

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

Además, toopoints, GeoJSON también admite LineStrings y polígonos. **LineStrings** representan una serie de dos o más puntos en el espacio y Hola segmentos de línea que conectan. En los datos geoespaciales, LineStrings son utilizadas toorepresent autopistas o ríos. Un elemento **Polygon** (polígono) es un área delimitada por puntos conectados que forman un elemento LineString cerrado. Polígonos son utilizadas toorepresent formaciones natural como lagos o políticos jurisdicciones como Estados y ciudades. Este es un ejemplo de un Polygon en Azure Cosmos DB. 

**Polygons en GeoJSON**

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
> Hola GeoJSON especificación requiere que para los polígonos válidos, hello último par de coordenadas proporcionada debe ser igual Hola como hello en primer lugar, toocreate una forma cerrada.
> 
> El orden de los puntos dentro de un elemento Polygon debe especificarse siguiendo el sentido contrario al de las agujas del reloj. Un polígono especificado en el orden de las agujas del reloj representa inverso de Hola de región de hello dentro de él.
> 
> 

En suma tooPoint, LineString y del polígono, GeoJSON también especifica representación Hola para saber cómo toogroup varias ubicaciones geoespaciales, así como la tooassociate propiedades arbitrarias con ubicación geográfica como una **característica**. Dado que estos objetos son JSON válidos, se pueden almacenar y procesar todos en Azure Cosmos DB. Sin embargo, Azure Cosmos DB solo admite la indexación automática de puntos.

### <a name="coordinate-reference-systems"></a>Sistemas de coordenadas de referencia
Puesto que forma Hola de tierra de hello es irregular, coordenadas de datos geoespaciales se representa en muchos sistemas de coordenadas de referencia (CR), cada uno con sus propios marcos de referencia y las unidades de medida. Por ejemplo, "Cuadrícula nacional de Bretaña" hello es un sistema de referencia es muy preciso para hello Reino Unido, pero no fuera de él. 

Hello CRS más populares en uso hoy en día es hello del sistema geodésico mundial [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Los dispositivos GPS y muchos servicios de mapeado como Google Maps y API de Bing Maps, usan WGS 84. Base de datos de Azure Cosmos admite indización y consulta de datos geoespaciales mediante Hola WGS 84 CRS. 

## <a name="creating-documents-with-spatial-data"></a>Creación de documentos con datos espaciales
Cuando haya creado los documentos que contienen valores de GeoJSON, se indizan automáticamente con un índice espacial en la directiva de indexación de acuerdo toohello de colección de Hola. Si está trabajando con un SDK de Azure Cosmos DB en un lenguaje de tipo dinámico como Python o Node.js, debe crear especificaciones GeoJSON válidas.

**Creación de documentos con datos geoespaciales en Node.js**

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

Si está trabajando con hello DocumentDB APIs, puede usar hello `Point` y `Polygon` clases dentro de hello `Microsoft.Azure.Documents.Spatial` información de ubicación de espacio de nombres tooembed dentro de los objetos de la aplicación. Estas clases ayudan a simplificar Hola serialización y deserialización de datos espaciales en GeoJSON.

**Creación de documentos con datos geoespaciales en .NET**

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

Si no tiene información de latitud y longitud de hello, pero tiene direcciones físicas de Hola o nombre de la ubicación como la ciudad o el país, puede buscar coordenadas real hello mediante el uso de un servicio de codificación geográfica como servicios de REST de mapas de Bing. Obtener más información acerca de la codificación geográfica de Bing Maps [aquí](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Consulta de tipos espaciales
Ahora que hemos llevado un vistazo a cómo los datos geoespaciales tooinsert, echemos un vistazo a cómo tooquery estos datos con la base de datos de Cosmos de Azure con SQL y LINQ.

### <a name="spatial-sql-built-in-functions"></a>Funciones integradas SQL espaciales
Base de datos de Azure Cosmos admite Hola siguiendo las funciones integradas de Open Geospatial Consortium (OGC) para realizar consultas geoespaciales. Para obtener más detalles sobre el conjunto completo de Hola de funciones integradas en hello lenguaje SQL, consulte demasiado[base de datos de consulta Azure Cosmos](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Uso</strong></td>
  <td><strong>Descripción</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Devuelve la distancia de hello entre expresiones de punto de GeoJSON, polígono o LineString Hola dos.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Devuelve una expresión booleana que indica si es Hola primer GeoJSON objeto (punto, polígono o LineString) dentro de hello segundo GeoJSON objeto (punto, polígono o LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Devuelve una expresión booleana que indica si se intersecan Hola dos GeoJSON objetos especificados (punto, polígono o LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Devuelve un valor booleano que indica si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Devuelve un valor JSON que contiene un valor booleano si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida y si no es válido, además Hola motivo como un valor de cadena.</td>
</tr>
</table>

Funciones espaciales pueden ser consultas de proximidad de tooperform utilizadas en los datos espaciales. Por ejemplo, aquí es una consulta que devuelve la que familia de todos los documentos que está dentro de 30 km de hello ubicación especificada mediante hello ST_DISTANCE función integrada. 

**Consultar**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Si incluye los índices espaciales en su directiva de indexación, a continuación, "consultas de distancia" se servirá eficazmente a través del índice de Hola. Para obtener más detalles sobre los índices espaciales, vea sección hello más adelante. Si no tienes espaciales índice para hello especifica las rutas de acceso, todavía puede realizar consultas espaciales especificando `x-ms-documentdb-query-enable-scan` establecida en el encabezado de solicitud con el valor de hello demasiado "verdadero". En. NET, esto puede hacerse por pasar Hola opcional **FeedOptions** tooqueries de argumento con [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) establecer tootrue. 

ST_WITHIN puede ser usado toocheck si se encuentra un punto dentro de un polígono. Normalmente polígonos son límites de toorepresent usado como códigos postales, los límites de estado o formaciones naturales. Nuevo si incluye los índices espaciales en su directiva de indexación, a continuación, "en" consultas se servirá eficazmente a través del índice de Hola. 

Argumentos de polígono en ST_WITHIN pueden contener solo un anillo único, es decir, Hola polígonos no debe contener vulnerabilidades en ellos. 

**Consultar**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Resultados**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Tipos de error de coincidencia de toohow similares funciona en la consulta de base de datos de Azure Cosmos, si el valor de la ubicación de hello especificado en el argumento está bien formado o no válido, a continuación, se evaluará demasiado**indefinido** Hola evaluada documento toobe omitido de Hola resultados de la consulta. Si la consulta no devuelve ningún resultado, ejecute toodebug ST_ISVALIDDETAILED ¿por qué tipo de hello spatail no es válido.     
> 
> 

Base de datos de Azure Cosmos también admite la realización de consultas inversas, es decir, es posible indizar polígonos o líneas de base de datos de Azure Cosmos y consultar las áreas de Hola que contenga un punto especificado. Este patrón es más frecuente en logística tooidentify por ejemplo, cuando un camión entra o sale de un área designada. 

**Consultar**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Resultados**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID y ST_ISVALIDDETAILED pueden ser utilizado toocheck si un objeto espacial es válido. Por ejemplo, hello después consulta comprueba la validez de Hola de un punto con un valor fuera del intervalo latitud (-132.8). ST_ISVALID devuelve un valor de tipo Boolean y Hola a ST_ISVALIDDETAILED devuelve un valor booleano y una cadena que contiene el motivo de hello ¿por qué se considera no válida.

** Consultar **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Resultados**

    [{
      "$1": false
    }]

Estas funciones también pueden ser polígonos de toovalidate usado. Por ejemplo, aquí usamos ST_ISVALIDDETAILED toovalidate un polígono que no está cerrado. 

**Consultar**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Resultados**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>Realizar consultas LINQ en hello SDK para .NET
Hola documentos .NET SDK también proveedores stub métodos `Distance()` y `Within()` para su uso dentro de las expresiones de LINQ. proveedor de DocumentDB LINQ Hello traduce estas llamadas toohello equivalente SQL función integrada llamadas al método (ST_DISTANCE y ST_WITHIN respectivamente). 

Este es un ejemplo de una consulta LINQ que busca todos los documentos en la colección de base de datos de Azure Cosmos Hola cuyo valor de "ubicación" está dentro de un radio de 30km de hello especificada punto mediante LINQ.

**Consulta LINQ de distancia**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

De forma similar, esta es una consulta para buscar todos los documentos de hello cuyo "ubicación" está dentro de hello especificado cuadro o polígono. 

**Consulta LINQ interna**

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


Ahora que hemos llevado un vistazo a cómo los documentos de tooquery mediante LINQ y SQL, echemos un vistazo a cómo tooconfigure base de datos de Azure Cosmos para los índices espaciales.

## <a name="indexing"></a>Indización
Tal y como se ha descrito en hello [esquema independiente de la indexación con base de datos de Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papel, diseñamos toobe de motor de base de datos de Azure Cosmos DB realmente independiente del esquema y proporcionar soporte de primera clase para JSON. motor de base de datos de escritura optimizado Hola de base de datos de Azure Cosmos entiende los datos espaciales (puntos, líneas y polígonos) representados en estándar de GeoJSON Hola.

En pocas palabras, geometry Hola se proyecta desde geodésicos coordenadas en un plano 2D, a continuación, dividir celdas mediante progresivamente un **quadtree**. Estas celdas están asignadas too1D basadas en ubicación de Hola de celda Hola dentro de un **curva de rellenado de espacio Hilbert**, que conserva una localidad de puntos. Además cuando se indizan los datos de ubicación, pasa por un proceso conocido como **teselación**, es decir, todas las celdas de Hola que forman una intersección una ubicación se identifican y se almacenan como claves de índice de base de datos de Azure Cosmos Hola. En el momento de la consulta, argumentos como puntos y polígonos también están divididas en mosaicos tooextract Hola intervalos de identificadores de celda relevante, utilizan datos de tooretrieve del índice de Hola.

Si especifica una directiva de indexación que incluye el índice espacial para / * (todas las rutas de acceso), a continuación, se indizan todos los puntos que se encuentra en la colección de Hola para consultas espaciales eficaces (ST_WITHIN y ST_DISTANCE). Los índices espaciales no tienen un valor de precisión y usan siempre un valor de precisión predeterminado.

> [!NOTE]
> Azure Cosmos DB admite la indexación automática de puntos, elementos Polygon y LineString.
> 
> 

Hello siguiente fragmento JSON muestra una directiva de indexación con habilitada la indización espacial, es decir, cualquier punto de GeoJSON que se encuentra dentro de los documentos para realizar consultas espaciales de índice. Si va a modificar Hola indización directiva mediante Hola Portal de Azure, puede especificar Hola después JSON para la indización de directiva tooenable espacial de indización en la colección.

**JSON de directiva de indexación de una colección con la característica espacial habilitada para puntos y elementos Polygon**

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

Este es un fragmento de código de .NET que muestra cómo toocreate una colección de los índices espaciales activado para todas las rutas de acceso que contiene puntos. 

**Creación de una colección con indexación espacial**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

Y aquí es cómo puede modificar una ventaja de tootake colección existente de índices espaciales sobre los puntos que se almacenan dentro de los documentos.

**Modificación de una colección ya existente con indexación espacial**

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
> Si ubicación hello GeoJSON valor dentro del documento de hello es incorrecto o no es válido, a continuación, lo no obtener indizará para realizar consultas espaciales. Puede validar los valores de ubicación mediante ST_ISVALID y ST_ISVALIDDETAILED.
> 
> Si la definición de la colección incluye una clave de partición, no se notifica el progreso de transformación de la indexación. 
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprender acerca de cómo tooget empezar con compatibilidad de geospatial en la base de datos de Azure Cosmos, puede:

* Comenzar a codificar con hello [ejemplos de código de Geospatial .NET en GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Obtener las manos en geospatial consultando al hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* Obtener más información sobre [Consultar Azure Cosmos DB](documentdb-sql-query.md)
* Obtener más información sobre [Directivas de indexación de Azure Cosmos DB](indexing-policies.md)

