---
title: Consultas SQL para la API de DocumentDB de Azure Cosmos DB | Microsoft Docs
description: "Más información sobre la sintaxis SQL, los conceptos de base de datos y las consultas SQL para Azure Cosmos DB. Puede usar SQL como lenguaje de consulta JSON en Azure Cosmos DB."
keywords: consulta sql, consultas sql, sintaxis sql, lenguaje de consulta json, conceptos de base de datos y consultas sql, funciones de agregado
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="6dcf2-105">Consultas SQL para la API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="6dcf2-106">Microsoft Azure Cosmos DB admite la consulta de documentos con SQL (lenguaje de consulta estructurado) como lenguaje de consulta de JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="6dcf2-107">Cosmos DB realmente no tiene esquemas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="6dcf2-108">En virtud de su compromiso con el modelo de datos JSON que se encuentra directamente en el motor de base de datos, proporciona índices automáticos de documentos JSON sin necesidad de un esquema explícito o de la creación de índices secundarios.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="6dcf2-109">Durante el diseño del lenguaje de consulta de Cosmos DB, teníamos dos objetivos en mente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="6dcf2-110">En lugar de inventar un nuevo lenguaje de consulta JSON, preferimos ofrecer compatibilidad con el lenguaje SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="6dcf2-111">SQL es uno de los lenguajes de consulta más familiares y populares.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="6dcf2-112">SQL de Cosmos DB proporciona un modelo de programación formal para consultas enriquecidas en documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="6dcf2-113">Igual que una base de datos de documentos JSON capaz de ejecutar JavaScript directamente en el motor de base de datos, queríamos usar el modelo de programación de JavaScript como base para nuestro lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="6dcf2-114">SQL de la API de DocumentDB se basa en el sistema de tipos de JavaScript, la evaluación de expresiones y la invocación de funciones.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="6dcf2-115">A su vez, esto proporciona un modelo de programación natural para proyecciones relacionales, navegación jerárquica por documentos JSON, autocombinaciones, consultas espaciales e invocación de funciones definidas por el usuario (UDF) escritas íntegramente en JavaScript, entre otras características.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="6dcf2-116">Creemos que estas capacidades son clave para reducir la fricción entre la aplicación y la base de datos, y que son cruciales para la productividad de los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="6dcf2-117">Se recomienda comenzar por ver el vídeo siguiente, donde Aravind Ramachandran muestra las capacidades de consulta de Cosmos DB y visitar [Query Playground](http://www.documentdb.com/sql/demo), donde puede probar Cosmos DB y ejecutar consultas SQL con nuestro conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="6dcf2-118">Luego, vuelva a este artículo, donde comenzamos con un tutorial de consulta SQL que le guiará a través de algunos documentos sencillos de JSON y comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="6dcf2-119"><a id="GettingStarted"></a>Introducción a los comandos SQL en Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="6dcf2-120">Para consultar SQL de Cosmos DB trabajando, empezaremos con unos documentos JSON sencillos y realizaremos algunas consultas fáciles con él.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="6dcf2-121">Tenga en cuenta estos dos documentos JSON sobre dos familias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="6dcf2-122">Con Cosmos DB no es preciso crear ningún esquema ni índice secundario de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="6dcf2-123">Simplemente tenemos que insertar los documentos JSON en una colección Cosmos DB y posteriormente realizar una consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="6dcf2-124">Aquí tenemos un documento JSON sencillo para la familia Andersen, los padres, los hijos (y sus mascotas), la dirección y la información de registro.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="6dcf2-125">El documento tiene cadenas, números, valores booleanos, matrices y propiedades anidadas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="6dcf2-126">**Documento**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="6dcf2-127">Aquí se muestra un segundo documento con una sutil diferencia: se usan `givenName` y `familyName` en lugar de `firstName` y `lastName`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="6dcf2-128">**Documento**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="6dcf2-129">Ahora realicemos algunas consultas con estos datos para entender algunos aspectos clave de SQL de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="6dcf2-130">Por ejemplo, la consulta siguiente devuelve los documentos en los que el campo id coincide con `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="6dcf2-131">Puesto que es `SELECT *`, la salida de la consulta es el documento JSON completo:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="6dcf2-132">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-133">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="6dcf2-134">Ahora preste atención al caso donde debemos cambiar el formato al resultado JSON con otra forma.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="6dcf2-135">Esta consulta proyecta un nuevo objeto JSON con dos campos seleccionados, Nombre y Ciudad, cuando la ciudad de la dirección tiene el mismo nombre que el estado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="6dcf2-136">En este caso, "NY, NY" coincide.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="6dcf2-137">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="6dcf2-138">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="6dcf2-139">La consulta siguiente devuelve todos los nombres proporcionados de los niños de la familia cuyo id. coincida con `WakefieldFamily`, ordenados por ciudad de residencia.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="6dcf2-140">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="6dcf2-141">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="6dcf2-142">Nos gustaría llamar la atención sobre algunos aspectos destacados del lenguaje de consulta de Cosmos DB a través de los ejemplos que hemos visto hasta el momento:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="6dcf2-143">Como SQL de la API de DocumentDB funciona con valores JSON, trata entidades en forma de árbol en lugar de filas y columnas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="6dcf2-144">Por consiguiente, el lenguaje permite que se haga referencia a los nodos del árbol a cualquier profundidad arbitraria, como `Node1.Node2.Node3…..Nodem`, de forma similar al lenguaje SQL relacional que hace alusión a la referencia dos partes de `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="6dcf2-145">El lenguaje de consulta estructurado trabaja con datos sin esquemas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="6dcf2-146">Por lo tanto, es necesario que el sistema de tipo se enlace dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="6dcf2-147">La misma expresión podría producir diversos tipos en distintos documentos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="6dcf2-148">El resultado de una consulta es un valor JSON válido, pero no se garantiza que sea de un esquema fijo.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="6dcf2-149">Cosmos DB solo admite documentos JSON estrictos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="6dcf2-150">Esto significa que el sistema de tipo y las expresiones se restringen para tratar únicamente tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="6dcf2-151">Para obtener más detalles, consulte la [especificación de JSON](http://www.json.org/).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="6dcf2-152">Una recopilación de Cosmos DB es un contenedor sin esquemas de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="6dcf2-153">Las relaciones en las entidades de datos dentro de los documentos de una colección y entre ellos se capturan de manera implícita por contención y no por relaciones entre clave principal y clave externa.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="6dcf2-154">Se trata de un aspecto importante que merece la pena señalar teniendo en cuenta las combinaciones internas descritas posteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="6dcf2-155"><a id="Indexing"></a> Indexación de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="6dcf2-156">Antes de entrar en la sintaxis de SQL de la API de DocumentDB, vale la pena explorar el diseño de indexación en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="6dcf2-157">El objetivo de los índices de base de datos es atender consultas en sus diversas formas con un consumo de los recursos mínimo (como CPU y entrada y salida) mientras se proporcionan un buen rendimiento y una latencia baja.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="6dcf2-158">A menudo, la elección del índice adecuado para consultar una base de datos requiere mucha planificación y experimentación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="6dcf2-159">Este enfoque plantea un desafío para las bases de datos sin esquemas en las que los datos no cumplen un esquema estricto y evolucionan rápidamente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="6dcf2-160">Por lo tanto, al diseñar el subsistema de indexación de Cosmos DB, establecemos los siguientes objetivos:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="6dcf2-161">Indexar documentos sin necesidad de esquema: el subsistema de indexación no requiere información de esquema alguna ni la realización de ninguna suposición sobre el esquema de los documentos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="6dcf2-162">Compatibilidad con consultas eficaces, enriquecidas jerárquicas y relacionales: el índice admite el lenguaje de consulta de Cosmos DB de manera eficaz, incluida la compatibilidad con proyecciones jerárquicas y relacionales.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="6dcf2-163">Compatibilidad con consultas coherentes frente a un volumen de escrituras sostenido: en el caso de las cargas de trabajo de alto rendimiento de escritura con consultas coherentes, el índice se actualiza paulatinamente, de forma eficaz y en línea frente a un volumen de escrituras sostenido.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="6dcf2-164">La actualización del índice coherente es crucial para atender las consultas en el nivel de coherencia en el que el usuario configura el servicio de documentos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="6dcf2-165">Compatibilidad con servicios multiinquilino: dado el modelo basado en la reserva para la regulación de recursos entre los inquilinos, se realizan actualizaciones de los índices sin sobrepasar el presupuesto de los recursos del sistema (CPU, memoria y operaciones de entrada y salida por segundo) asignadas por réplica.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="6dcf2-166">Eficacia de almacenamiento: para obtener rentabilidad, se enlaza la sobrecarga de almacenamiento en el disco del índice y es predecible.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="6dcf2-167">Esto es fundamental porque Cosmos DB permite que el desarrollador haga concesiones basadas en el costo entre la sobrecarga de índices y el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="6dcf2-168">Consulte los [ejemplos de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) en MSDN para ver casos en los que se muestra cómo configurar la directiva de indexación para una colección.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="6dcf2-169">Adentrémonos ahora en los detalles de la sintaxis de SQL de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="6dcf2-170"><a id="Basics"></a>Conceptos básicos de una consulta SQL de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="6dcf2-171">Todas las consultas constan de una cláusula SELECT y cláusulas FROM y WHERE opcionales por estándares ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="6dcf2-172">Normalmente, para cada consulta, se enumera el origen de la cláusula FROM.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="6dcf2-173">A continuación, el filtro de la cláusula WHERE se aplica en el origen para recuperar un subconjunto de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="6dcf2-174">Por último, la cláusula SELECT se usa para proyectar los valores JSON solicitados en la lista seleccionada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="6dcf2-175"><a id="FromClause"></a>Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="6dcf2-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="6dcf2-176">La cláusula `FROM <from_specification>` es opcional, a menos que el origen se filtre o se proyecte posteriormente en la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="6dcf2-177">El objetivo de esta cláusula es especificar el origen de datos sobre el que debe operar la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="6dcf2-178">Normalmente, toda la recopilación es el origen pero, en su lugar, puede especificarse un subconjunto de la recopilación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="6dcf2-179">Una consulta como `SELECT * FROM Families` indica que toda la colección Families es el origen sobre el que se va a realizar la enumeración.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="6dcf2-180">Se puede usar una RAÍZ de identificador especial para representar la colección en lugar de usar el nombre de la colección.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="6dcf2-181">La lista siguiente contiene las reglas que se aplican por consulta:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="6dcf2-182">Puede establecerse para la colección un alias como `SELECT f.id FROM Families AS f`, o simplemente `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="6dcf2-183">Aquí, `f` es el equivalente de `Families`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="6dcf2-184">`AS` es una palabra clave opcional para establecer un alias para el identificador.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="6dcf2-185">Una vez establecido un alias, el origen original no puede enlazarse.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="6dcf2-186">Por ejemplo, `SELECT Families.id FROM Families f` no es válido sintácticamente porque el identificador "Families" no puede resolverse.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="6dcf2-187">Todas las propiedades a las que es necesario hacer referencia deben estar completas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="6dcf2-188">A falta de un cumplimiento del esquema estricto, esto se impone para evitar cualquier enlace ambiguo.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="6dcf2-189">Por lo tanto, `SELECT id FROM Families f` no es válido sintácticamente porque la propiedad `id` no está enlazada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="6dcf2-190">Subdocumentos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-190">Subdocuments</span></span>
<span data-ttu-id="6dcf2-191">El origen también se puede reducir a un subconjunto más pequeño.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="6dcf2-192">Por ejemplo, para enumerar únicamente un subárbol en cada documento, la subraíz podría convertirse en el origen, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="6dcf2-193">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="6dcf2-194">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="6dcf2-195">Aunque en el ejemplo anterior se usa una matriz como origen, también se podría usar un objeto como origen, que es lo que se muestra en el ejemplo siguiente: cualquier valor JSON válido (no sin definir) que se pueda encontrar en el origen se considera para su inclusión en el resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="6dcf2-196">Si algunas familias no tienen un valor `address.state` , se excluyen del resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="6dcf2-197">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="6dcf2-198">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="6dcf2-199"><a id="WhereClause"></a>Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="6dcf2-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="6dcf2-200">La cláusula WHERE (**`WHERE <filter_condition>`**) es opcional.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="6dcf2-201">Especifica las condiciones de que los documentos JSON proporcionados por el origen deben satisfacer para incluirse como parte del resultado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="6dcf2-202">Cualquier documento JSON debe evaluar las condiciones especificadas en "true" para su consideración para el resultado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="6dcf2-203">La capa de índice usa la cláusula WHERE para determinar el subconjunto más pequeño absoluto de documentos de origen que pueden formar parte del resultado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="6dcf2-204">En la consulta siguiente se solicitan documentos que contienen una propiedad de nombre cuyo valor es `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="6dcf2-205">Cualquier otro documento que no tenga una propiedad de nombre o en el que el valor no coincida con `AndersenFamily` se excluye.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="6dcf2-206">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-207">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="6dcf2-208">En el ejemplo anterior se mostraba una sencilla consulta de igualdad.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="6dcf2-209">SQL de la API de DocumentDB también admite diversas expresiones escalares.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="6dcf2-210">Las que más se suelen usar son binarias y unarias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="6dcf2-211">Las referencias de propiedad del objeto JSON de origen también son expresiones válidas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="6dcf2-212">Actualmente se admiten los siguientes operadores binarios y pueden usarse en consultas como se muestra en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="6dcf2-213">Aritméticos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="6dcf2-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="6dcf2-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dcf2-215">Bit a bit</span><span class="sxs-lookup"><span data-stu-id="6dcf2-215">Bitwise</span></span></td>    
<td><span data-ttu-id="6dcf2-216">|, &, ^, <<, >>, >>> (desplazamiento a la derecha con relleno de ceros)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dcf2-217">Lógicos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-217">Logical</span></span></td>
<td><span data-ttu-id="6dcf2-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="6dcf2-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dcf2-219">De comparación</span><span class="sxs-lookup"><span data-stu-id="6dcf2-219">Comparison</span></span></td>    
<td><span data-ttu-id="6dcf2-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="6dcf2-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6dcf2-221">Cadena</span><span class="sxs-lookup"><span data-stu-id="6dcf2-221">String</span></span></td>    
<td><span data-ttu-id="6dcf2-222">|| (concatenar)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="6dcf2-223">Echemos un vistazo a algunas consultas usando operadores binarios.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="6dcf2-224">También se admiten los operadores unarios +,-, ~ y NOT, y se pueden usar dentro de consultas como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="6dcf2-225">Además de los operadores unarios y binarios, también se permiten referencias de propiedad.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="6dcf2-226">Por ejemplo, `SELECT * FROM Families f WHERE f.isRegistered` devuelve el documento JSON que contenga la propiedad `isRegistered` en la que el valor de la propiedad sea igual al valor `true` JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="6dcf2-227">Cualquier otro valor (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) hace que el documento de origen se excluya del resultado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="6dcf2-228">Operadores de igualdad y de comparación</span><span class="sxs-lookup"><span data-stu-id="6dcf2-228">Equality and comparison operators</span></span>
<span data-ttu-id="6dcf2-229">En la siguiente tabla se muestra el resultado de las comparaciones de igualdad en el lenguaje SQL de la API de DocumentDB entre dos tipos JSON cualesquiera.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-233">
            <strong>Booleano</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-234">
            <strong>Número</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-235">
            <strong>Cadena</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-236">
            <strong>Objeto</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="6dcf2-237">
            <strong>Matriz</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="6dcf2-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-254">
            <strong>Booleano<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="6dcf2-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-262">
            <strong>Número<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="6dcf2-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-270">
            <strong>Cadena<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="6dcf2-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-278">
            <strong>Objeto<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="6dcf2-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="6dcf2-286">
            <strong>Matriz<strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="6dcf2-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="6dcf2-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="6dcf2-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="6dcf2-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="6dcf2-294">Para otros operadores de comparación como >, >=, !=, < y <=, se aplican las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="6dcf2-295">La comparación entre los tipos da lugar a Undefined.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="6dcf2-296">La comparación entre dos objetos o dos matrices da lugar a Undefined.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="6dcf2-297">Si el resultado de la expresión escalar del filtro es Undefined, el documento correspondiente no se incluiría en el resultado, pues Undefined no es igual lógicamente a "true".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="6dcf2-298">Palabra clave BETWEEN</span><span class="sxs-lookup"><span data-stu-id="6dcf2-298">BETWEEN keyword</span></span>
<span data-ttu-id="6dcf2-299">También puede usar la palabra clave BETWEEN para expresar consultas en intervalos de valores como en ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="6dcf2-300">BETWEEN puede utilizarse con cadenas o números.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="6dcf2-301">Por ejemplo, esta consulta devuelve todos los documentos de la familia en los que el curso del primer hijo se encuentra entre 1 y 5 (ambos inclusive).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="6dcf2-302">Al contrario que en ANSI SQL, también se puede usar la cláusula BETWEEN en la cláusula FROM, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="6dcf2-303">Para que la consulta se ejecute de forma más rápida, no olvide crear una directiva de indización que use un tipo de índice de intervalo en cualquier ruta o propiedad numérica que se filtre en la cláusula BETWEEN.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="6dcf2-304">La principal diferencia entre usar BETWEEN en la API de DocumentDB y SQL ANSI es que puede expresar consultas por rangos en propiedades de tipos mixtos. Por ejemplo, "grade" podría ser un número (5) en algunos documentos y una cadena ("grade4") en otros.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="6dcf2-305">En estos casos, al igual que en JavaScript, una comparación entre dos tipos distintos da como resultado "undefined" y el documento se omitirá.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="6dcf2-306">Operadores lógicos (Y, O y NO)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="6dcf2-307">Los operadores lógicos operan en valores booleanos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="6dcf2-308">Las tablas de verdad lógica para estos operadores se muestran en las siguientes tablas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="6dcf2-309">OR</span><span class="sxs-lookup"><span data-stu-id="6dcf2-309">OR</span></span> | <span data-ttu-id="6dcf2-310">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-310">True</span></span> | <span data-ttu-id="6dcf2-311">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-311">False</span></span> | <span data-ttu-id="6dcf2-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dcf2-313">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-313">True</span></span> |<span data-ttu-id="6dcf2-314">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-314">True</span></span> |<span data-ttu-id="6dcf2-315">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-315">True</span></span> |<span data-ttu-id="6dcf2-316">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-316">True</span></span> |
| <span data-ttu-id="6dcf2-317">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-317">False</span></span> |<span data-ttu-id="6dcf2-318">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-318">True</span></span> |<span data-ttu-id="6dcf2-319">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-319">False</span></span> |<span data-ttu-id="6dcf2-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-320">Undefined</span></span> |
| <span data-ttu-id="6dcf2-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-321">Undefined</span></span> |<span data-ttu-id="6dcf2-322">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-322">True</span></span> |<span data-ttu-id="6dcf2-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-323">Undefined</span></span> |<span data-ttu-id="6dcf2-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-324">Undefined</span></span> |

| <span data-ttu-id="6dcf2-325">Y</span><span class="sxs-lookup"><span data-stu-id="6dcf2-325">AND</span></span> | <span data-ttu-id="6dcf2-326">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-326">True</span></span> | <span data-ttu-id="6dcf2-327">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-327">False</span></span> | <span data-ttu-id="6dcf2-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6dcf2-329">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-329">True</span></span> |<span data-ttu-id="6dcf2-330">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-330">True</span></span> |<span data-ttu-id="6dcf2-331">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-331">False</span></span> |<span data-ttu-id="6dcf2-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-332">Undefined</span></span> |
| <span data-ttu-id="6dcf2-333">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-333">False</span></span> |<span data-ttu-id="6dcf2-334">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-334">False</span></span> |<span data-ttu-id="6dcf2-335">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-335">False</span></span> |<span data-ttu-id="6dcf2-336">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-336">False</span></span> |
| <span data-ttu-id="6dcf2-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-337">Undefined</span></span> |<span data-ttu-id="6dcf2-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-338">Undefined</span></span> |<span data-ttu-id="6dcf2-339">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-339">False</span></span> |<span data-ttu-id="6dcf2-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-340">Undefined</span></span> |

| <span data-ttu-id="6dcf2-341">NO</span><span class="sxs-lookup"><span data-stu-id="6dcf2-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="6dcf2-342">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-342">True</span></span> |<span data-ttu-id="6dcf2-343">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-343">False</span></span> |
| <span data-ttu-id="6dcf2-344">False</span><span class="sxs-lookup"><span data-stu-id="6dcf2-344">False</span></span> |<span data-ttu-id="6dcf2-345">True</span><span class="sxs-lookup"><span data-stu-id="6dcf2-345">True</span></span> |
| <span data-ttu-id="6dcf2-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-346">Undefined</span></span> |<span data-ttu-id="6dcf2-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="6dcf2-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="6dcf2-348">Palabra clave IN</span><span class="sxs-lookup"><span data-stu-id="6dcf2-348">IN keyword</span></span>
<span data-ttu-id="6dcf2-349">La palabra clave IN puede usarse para comprobar si un valor especificado coincide con algún valor de una lista.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="6dcf2-350">Por ejemplo, esta consulta devuelve todos los documentos de la familia en los que el identificador sea "WakefieldFamily" o "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="6dcf2-351">Este ejemplo devuelve todos los documentos en los que el estado es cualquiera de los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="6dcf2-352">Operadores ternario (?) y de fusión (??)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="6dcf2-353">El operador ternario y el operador de combinación pueden usarse para crear expresiones condicionales, de forma similar a lenguajes de programación populares como C# y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="6dcf2-354">El operador ternario (?) puede ser muy útil al construir nuevas propiedades JSON sobre la marcha.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="6dcf2-355">Así, ahora puede escribir consultas para clasificar los niveles de clase en formato de lenguaje natural, por ejemplo Principiante/Intermedio/Avanzado, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="6dcf2-356">También puede anidar las llamadas al operador como en la consulta siguiente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="6dcf2-357">Como ocurre con otros operadores de consulta, si las propiedades a las que se hace referencia en la expresión condicional faltan en cualquier documento, o si los tipos que se comparan son diferentes, esos documentos se excluyen de los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="6dcf2-358">El operador de fusión (??) se puede usar para comprobar eficazmente la presencia de una propiedad</span><span class="sxs-lookup"><span data-stu-id="6dcf2-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="6dcf2-359">(es decir, si esta se ha definido) en un documento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-359">is defined) in a document.</span></span> <span data-ttu-id="6dcf2-360">Esto es útil cuando se consultan datos semiestructurados o de tipos combinados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="6dcf2-361">Por ejemplo, esta consulta devuelve el valor "lastName" si está presente o "surname" si no lo está.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="6dcf2-362"><a id="EscapingReservedKeywords"></a>Descriptor de acceso de propiedad entre comillas</span><span class="sxs-lookup"><span data-stu-id="6dcf2-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="6dcf2-363">También es posible obtener acceso a las propiedades mediante el operador de la propiedad entre comillas `[]`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="6dcf2-364">Por ejemplo, `SELECT c.grade` and `SELECT c["grade"]` son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="6dcf2-365">Esta sintaxis es útil cuando se necesita crear una secuencia de escape para una propiedad que contiene espacios en blanco, caracteres especiales, o que comparte el nombre con una palabra clave SQL o una palabra reservada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="6dcf2-366"><a id="SelectClause"></a>Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="6dcf2-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="6dcf2-367">La cláusula SELECT (**`SELECT <select_list>`**) es obligatoria y especifica los valores que se recuperan de la consulta, de la misma forma que en ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="6dcf2-368">El subconjunto que se ha filtrado en la parte superior de los documentos de origen pasa a la fase de proyección, en la cual se recuperan los valores JSON especificados y se construye un nuevo objeto JSON para cada una de las entradas que pasan a él.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="6dcf2-369">En el ejemplo siguiente se muestra una consulta SELECT típica:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="6dcf2-370">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-371">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="6dcf2-372">Propiedades anidadas</span><span class="sxs-lookup"><span data-stu-id="6dcf2-372">Nested properties</span></span>
<span data-ttu-id="6dcf2-373">En el ejemplo siguiente, se proyectan dos propiedades anidadas, `f.address.state` and `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="6dcf2-374">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-375">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="6dcf2-376">La proyección también admite expresiones de JSON, como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="6dcf2-377">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-378">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="6dcf2-379">Analicemos el rol que `$1` tiene aquí.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="6dcf2-380">La cláusula `SELECT` debe crear un objeto JSON y, como no se proporciona ninguna clave, usamos nombres de variable de argumentos implícitos que empiezan por `$1`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="6dcf2-381">Por ejemplo, esta consulta devuelve dos variables de argumentos implícitos, etiquetadas como `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="6dcf2-382">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-383">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="6dcf2-384">Establecimiento de alias</span><span class="sxs-lookup"><span data-stu-id="6dcf2-384">Aliasing</span></span>
<span data-ttu-id="6dcf2-385">Ampliemos ahora el ejemplo anterior con un establecimiento de alias explícito para valores.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="6dcf2-386">AS es la palabra clave usada para el establecimiento de alias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="6dcf2-387">Es opcional, como se muestra al proyectarse el segundo valor como `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="6dcf2-388">En caso de que una consulta tenga dos propiedades con el mismo nombre, el establecimiento de alias debe usarse para cambiar el nombre de las propiedades de modo que se elimine su ambigüedad en el resultado proyectado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="6dcf2-389">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-390">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="6dcf2-391">Expresiones escalares</span><span class="sxs-lookup"><span data-stu-id="6dcf2-391">Scalar expressions</span></span>
<span data-ttu-id="6dcf2-392">Además de las referencias de propiedad, la cláusula SELECT también admite expresiones escalares como constantes, expresiones aritméticas, expresiones lógicas, etc. Por ejemplo, aquí hay una sencilla consulta "Hello World".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="6dcf2-393">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="6dcf2-394">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="6dcf2-395">A continuación se muestra un ejemplo más complejo que usa una expresión escalar.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="6dcf2-396">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="6dcf2-397">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="6dcf2-398">En el ejemplo siguiente, el resultado de la expresión escalar es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="6dcf2-399">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="6dcf2-400">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="6dcf2-401">Creación de objetos y matrices</span><span class="sxs-lookup"><span data-stu-id="6dcf2-401">Object and array creation</span></span>
<span data-ttu-id="6dcf2-402">Otra característica clave del lenguaje SQL de la API de DocumentDB es la creación de matrices u objetos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="6dcf2-403">En el ejemplo anterior, observe que creamos un nuevo objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="6dcf2-404">De manera similar, también se pueden construir matrices como se muestra en los siguientes ejemplos:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="6dcf2-405">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="6dcf2-406">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="6dcf2-407"><a id="ValueKeyword"></a>Palabra clave VALUE</span><span class="sxs-lookup"><span data-stu-id="6dcf2-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="6dcf2-408">La palabra clave **VALUE** proporciona una forma de devolver un valor JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="6dcf2-409">Por ejemplo, la consulta que se muestra a continuación devuelve la expresión escalar `"Hello World"`, en lugar de `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="6dcf2-410">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="6dcf2-411">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="6dcf2-412">La siguiente consulta devuelve el valor JSON sin la etiqueta `"address"` en los resultados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="6dcf2-413">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="6dcf2-414">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="6dcf2-415">El ejemplo siguiente se amplía para mostrar cómo devolver valores primitivos JSON (el nivel de hoja del árbol JSON).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="6dcf2-416">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="6dcf2-417">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="6dcf2-418">Operador *</span><span class="sxs-lookup"><span data-stu-id="6dcf2-418">* Operator</span></span>
<span data-ttu-id="6dcf2-419">Se admite el operador especial (*) para proyectar el documento tal cual.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="6dcf2-420">Al usarse, debe ser el único campo proyectado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="6dcf2-421">Aunque una consulta como `SELECT * FROM Families f` es válida, `SELECT VALUE * FROM Families f ` y `SELECT *, f.id FROM Families f ` no lo son.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="6dcf2-422">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="6dcf2-423">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="6dcf2-424"><a id="TopKeyword"></a>Operador TOP</span><span class="sxs-lookup"><span data-stu-id="6dcf2-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="6dcf2-425">La palabra clave TOP se puede usar para limitar la cantidad de valores de una consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="6dcf2-426">Cuando se usa TOP junto con la cláusula ORDER BY, el conjunto de resultados se limita a los primeros N valores ordenados; de otro modo, devuelve los primeros N resultados en orden indefinido.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="6dcf2-427">Como procedimiento recomendado, en una instrucción SELECT, siempre use una cláusula ORDER BY con la cláusula TOP.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="6dcf2-428">Esta es la única forma previsible de indicar qué filas afecta TOP.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="6dcf2-429">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="6dcf2-430">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="6dcf2-431">TOP se puede usar con un valor constante (como se muestra anteriormente) o con un valor variable usando consultas con parámetros.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="6dcf2-432">Si desea obtener más información, consulte las consultas con parámetros que aparecen a continuación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="6dcf2-433"><a id="Aggregates"></a>Funciones de agregado</span><span class="sxs-lookup"><span data-stu-id="6dcf2-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="6dcf2-434">También puede realizar agregaciones en la cláusula `SELECT`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="6dcf2-435">Las funciones de agregado realizan un cálculo en un conjunto de valores y devuelven un valor único.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="6dcf2-436">Por ejemplo, la consulta siguiente devuelve el número de documentos de la familia dentro de la colección.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="6dcf2-437">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="6dcf2-438">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="6dcf2-439">También puede devolver el valor escalar del agregado mediante la palabra clave `VALUE`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="6dcf2-440">Por ejemplo, la siguiente consulta devuelve el número de valores como un único número:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="6dcf2-441">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="6dcf2-442">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="6dcf2-443">También puede realizar agregados en combinación con filtros.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="6dcf2-444">Por ejemplo, la consulta siguiente devuelve aquellos documentos con dirección en el estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="6dcf2-445">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="6dcf2-446">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="6dcf2-447">En la tabla siguiente se muestra la lista de funciones de agregado compatibles de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="6dcf2-448">`SUM`y `AVG` se aplican a valores numéricos, mientras que `COUNT`, `MIN` y `MAX` se pueden aplicar a números, cadenas, y valores booleanos y NULL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="6dcf2-449">Uso</span><span class="sxs-lookup"><span data-stu-id="6dcf2-449">Usage</span></span> | <span data-ttu-id="6dcf2-450">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcf2-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="6dcf2-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="6dcf2-451">COUNT</span></span> | <span data-ttu-id="6dcf2-452">Devuelve el número de elementos de la expresión.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="6dcf2-453">SUM</span><span class="sxs-lookup"><span data-stu-id="6dcf2-453">SUM</span></span>   | <span data-ttu-id="6dcf2-454">Devuelve la suma de todos los valores de la expresión.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="6dcf2-455">MÍN</span><span class="sxs-lookup"><span data-stu-id="6dcf2-455">MIN</span></span>   | <span data-ttu-id="6dcf2-456">Devuelve el valor mínimo de la expresión.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="6dcf2-457">MÁX</span><span class="sxs-lookup"><span data-stu-id="6dcf2-457">MAX</span></span>   | <span data-ttu-id="6dcf2-458">Devuelve el valor máximo de la expresión.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="6dcf2-459">MEDIA</span><span class="sxs-lookup"><span data-stu-id="6dcf2-459">AVG</span></span>   | <span data-ttu-id="6dcf2-460">Devuelve la media de los valores de la expresión.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="6dcf2-461">Las funciones de agregado también se pueden aplicar a los resultados de una iteración de la matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="6dcf2-462">Para más información, vea [Iteración de matriz en consultas](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="6dcf2-463">Al usar el Explorador de consultas de Azure Portal, tenga en cuenta que las consultas de agregación pueden devolver resultados agregados parcialmente a través de una página de consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="6dcf2-464">Los SDK generan un único valor acumulado en todas las páginas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="6dcf2-465">Para realizar consultas de agregación mediante código, necesita .NET SDK 1.12.0, .NET Core SDK 1.1.0 o Java SDK 1.9.5 o superior.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="6dcf2-466"><a id="OrderByClause"></a>Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="6dcf2-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="6dcf2-467">Al igual que en ANSI SQL, puede incluir una cláusula Order By opcional al realizar la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="6dcf2-468">La cláusula puede incluir un argumento ASC o DESC opcional para especificar el orden en que se deben recuperar los resultados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="6dcf2-469">Por ejemplo, aquí hay una consulta que recupera las familias ordenadas por nombre de la ciudad de residencia.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="6dcf2-470">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="6dcf2-471">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="6dcf2-472">Y la siguiente es una consulta que recupera las familias ordenadas por fecha de creación, que se almacena como un número que representa el tiempo epoch, es decir, el tiempo transcurrido desde el 1 de enero de 1970, en segundos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="6dcf2-473">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="6dcf2-474">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="6dcf2-475"><a id="Advanced"></a>Conceptos avanzados de base de datos y consultas SQL</span><span class="sxs-lookup"><span data-stu-id="6dcf2-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="6dcf2-476"><a id="Iteration"></a>Iteración</span><span class="sxs-lookup"><span data-stu-id="6dcf2-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="6dcf2-477">Se ha agregado una nueva construcción mediante la palabra clave **IN** en SQL de la API de DocumentDB que proporcionar compatibilidad con la iteración en las matrices JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="6dcf2-478">El origen FROM proporciona compatibilidad con la iteración.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="6dcf2-479">Empecemos con el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-479">Let's start with the following example:</span></span>

<span data-ttu-id="6dcf2-480">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="6dcf2-481">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="6dcf2-482">Analicemos ahora otra consulta que realice una iteración sobre elementos secundarios de la recopilación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="6dcf2-483">Observe la diferencia en la matriz de salida.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-483">Note the difference in the output array.</span></span> <span data-ttu-id="6dcf2-484">En este ejemplo se divide `children` y se reducen los resultados a una sola matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="6dcf2-485">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="6dcf2-486">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="6dcf2-487">Esto puede usarse más veces para filtrar por cada entrada individual de la matriz como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="6dcf2-488">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="6dcf2-489">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="6dcf2-490">También puede aplicar agregaciones al resultado de la iteración de la matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="6dcf2-491">Por ejemplo, la consulta siguiente cuenta el número de hijos entre todas las familias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="6dcf2-492">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="6dcf2-493">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="6dcf2-494"><a id="Joins"></a>Combinaciones</span><span class="sxs-lookup"><span data-stu-id="6dcf2-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="6dcf2-495">En una base de datos relacional, la necesidad de combinar en tablas es importante.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="6dcf2-496">Es la consecuencia lógica de diseñar esquemas normalizados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="6dcf2-497">Al contrario que esto, la API de DocumentDB aborda el modelo de datos desnormalizado de documentos sin esquemas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="6dcf2-498">Este es el equivalente lógico de una "autocombinación".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="6dcf2-499">La sintaxis que admite el lenguaje es <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="6dcf2-500">Generalmente, esto devuelve un conjunto de **N** tuplas (tupla con **N** valores).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="6dcf2-501">Cada tupla tiene valores generados por sus respectivos conjuntos en iteración de todos los alias de colección.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="6dcf2-502">En otras palabras, se trata de un producto cruzado completo de los conjuntos que participan en la combinación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="6dcf2-503">En los ejemplos siguientes se muestra cómo funciona la cláusula JOIN.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="6dcf2-504">En el siguiente ejemplo, el resultado está vacío porque el producto cruzado de cada documento del origen y un conjunto vacío está vacío.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="6dcf2-505">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="6dcf2-506">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="6dcf2-507">En el ejemplo siguiente, la combinación se realiza entre la raíz del documento y la subraíz de `children`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="6dcf2-508">Es un producto cruzado entre dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="6dcf2-509">El hecho de que los elementos secundarios sean una matriz no funciona en JOIN porque abordamos una sola raíz que es la matriz secundaria.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="6dcf2-510">Así pues, en el resultado se incluyen únicamente dos resultados, pues el producto cruzado de cada documento con la matriz produce exactamente solo un documento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="6dcf2-511">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="6dcf2-512">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="6dcf2-513">En el ejemplo siguiente se muestra una combinación más convencional:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="6dcf2-514">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="6dcf2-515">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="6dcf2-516">Lo primero que hay que tener en cuenta es que `from_source` de la cláusula **JOIN** es un iterador.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="6dcf2-517">Por lo tanto, el flujo en este caso es como sigue:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="6dcf2-518">Amplía cada elemento secundario **c** en la matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="6dcf2-519">Aplique un producto cruzado con la raíz del documento **f** con cada elemento secundario **c** del que se quitó el formato en el primer paso.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="6dcf2-520">Por último, proyecte solo la propiedad de nombre **f** del objeto raíz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="6dcf2-521">El primer documento (`AndersenFamily`) contiene únicamente un elemento secundario, por lo que el conjunto de resultados contiene solo un objeto correspondiente a este documento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="6dcf2-522">El segundo documento (`WakefieldFamily`) contiene dos elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="6dcf2-523">De este modo, el producto cruzado produce un objeto independiente para cada elemento secundario, lo que da lugar a dos objetos, uno para cada elemento secundario correspondiente a este documento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="6dcf2-524">Los campos de raíz de estos dos documentos son los mismos, justo como se esperaría en un producto cruzado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="6dcf2-525">La utilidad real de JOIN es la formación de tuplas a partir del producto cruzado con una forma que de otro modo es difícil de proyectar.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="6dcf2-526">Además, como se ve en el siguiente ejemplo, podría filtrarse por la combinación de una tupla que permite que el usuario elija una condición satisfecha por las tuplas en general.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="6dcf2-527">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="6dcf2-528">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="6dcf2-529">Este ejemplo es una ampliación natural del anterior y realiza una combinación doble.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="6dcf2-530">De este modo, el producto cruzado se puede ver como el pseudocódigo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="6dcf2-531">`AndersenFamily` tiene un hijo que tiene una mascota.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="6dcf2-532">De esta manera, el producto cruzado produce una fila (1\*1\*1) a partir de esta familia.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="6dcf2-533">La familia Wakefield tiene, sin embargo, dos hijos, pero solo uno, "Jesse", tiene mascotas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="6dcf2-534">Pero Jesse tiene dos mascotas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-534">Jesse has two pets though.</span></span> <span data-ttu-id="6dcf2-535">Así pues, el producto cruzado produce 1\*1\*2 = 2 filas a partir de esta familia.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="6dcf2-536">En el ejemplo siguiente, hay un filtro adicional en `pet`</span><span class="sxs-lookup"><span data-stu-id="6dcf2-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="6dcf2-537">Este excluye todas las tuplas donde el nombre de mascota no sea "Shadow".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="6dcf2-538">Tenga en cuenta que podemos crear tuplas a partir de matrices, filtrar por cualquiera de los elementos de la tupla y proyectar cualquier combinación de los elementos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="6dcf2-539">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="6dcf2-540">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="6dcf2-541"><a id="JavaScriptIntegration"></a>Integración de JavaScript</span><span class="sxs-lookup"><span data-stu-id="6dcf2-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="6dcf2-542">Azure Cosmos DB proporciona un modelo de programación para ejecutar una lógica de aplicación basada en JavaScript directamente en las recopilaciones en términos de procedimientos y desencadenadores almacenados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="6dcf2-543">Esto les proporciona:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-543">This allows for both:</span></span>

* <span data-ttu-id="6dcf2-544">La posibilidad de realizar operaciones CRUD transaccionales de alto rendimiento y consultas en los documentos de una colección en virtud de una mayor integración del tiempo de ejecución de JavaScript directamente en el motor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="6dcf2-545">Un modelo natural de flujo de control, ámbito variable, asignación e integración de primitivas de control de excepciones con transacciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="6dcf2-546">Para obtener más detalles sobre la compatibilidad de Azure Cosmos DB con la integración de JavaScript, consulte la documentación de programación del servidor de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="6dcf2-547"><a id="UserDefinedFunctions"></a>Funciones definidas por el usuario (UDF)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="6dcf2-548">Junto con los tipos ya definidos en este artículo, el lenguaje SQL de la API de DocumentDB ofrece compatibilidad para las funciones definidas por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="6dcf2-549">En particular, se admiten las UDF escalares allí donde los desarrolladores puedan proporcionar cero o muchos argumentos y devolver un solo resultado de argumento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="6dcf2-550">Cada uno de estos argumentos se comprueba para ver si se trata de valores JSON válidos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="6dcf2-551">La sintaxis SQL de la API de DocumentDB se amplía para admitir lógica de aplicación personalizada mediante estas funciones definidas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="6dcf2-552">Las funciones definidas por el usuario pueden registrarse con la API de DocumentDB y, a continuación, se puede hacer referencia a ellas como parte de una consulta de SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="6dcf2-553">De hecho, las UDF están exquisitamente diseñadas para su invocación por parte de las consultas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="6dcf2-554">Como resultado de esta opción, las UDF no tienen acceso al objeto de contexto que los otros tipos de JavaScript (procedimientos y desencadenadores almacenados) tienen.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="6dcf2-555">Puesto que las consultas se ejecutan como de solo lectura, pueden ejecutarse en réplicas principales o secundarias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="6dcf2-556">Por consiguiente, las UDF están diseñadas para ejecutarse en réplicas secundarias, a diferencia de otros tipos de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="6dcf2-557">A continuación, vemos un ejemplo de cómo puede registrarse una UDF en la base de datos de Cosmos DB, concretamente en una recopilación de documentos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="6dcf2-558">El ejemplo anterior crea una UDF cuyo nombre es `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="6dcf2-559">Acepta dos valores de cadena JSON, `input` and `pattern` , y comprueba si el primero coincide con el patrón especificado en el segundo mediante la función string.match() de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="6dcf2-560">Ahora podemos usar esta UDF en una consulta de una proyección.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="6dcf2-561">Las UDF deben estar calificadas con el prefijo, que distingue mayúsculas de minúsculas, "udf."</span><span class="sxs-lookup"><span data-stu-id="6dcf2-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="6dcf2-562">cuando se las llama desde las consultas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="6dcf2-563">Antes del 17/03/2015, Cosmos DB admitía las llamadas de UDF sin el prefijo "udf."</span><span class="sxs-lookup"><span data-stu-id="6dcf2-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="6dcf2-564">al igual que SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="6dcf2-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="6dcf2-565">Este patrón de llamada está desusado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="6dcf2-566">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="6dcf2-567">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="6dcf2-568">La UDF también puede usarse en un filtro tal como se muestra en el ejemplo siguiente, calificado igualmente con el prefijo "udf."</span><span class="sxs-lookup"><span data-stu-id="6dcf2-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="6dcf2-569">prefijo:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-569">prefix:</span></span>

<span data-ttu-id="6dcf2-570">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="6dcf2-571">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="6dcf2-572">Básicamente, las UDF son expresiones escalares válidas y pueden usarse en ambas proyecciones y filtros.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="6dcf2-573">Para expandir el poder de las UDF, echemos un vistazo a otro ejemplo con lógica condicional:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="6dcf2-574">A continuación se muestra un ejemplo que ejerce la UDF.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="6dcf2-575">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="6dcf2-576">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="6dcf2-577">Al igual que en los ejemplos anteriores se muestran casos, las UDF integran el poder del lenguaje de JavaScript con el lenguaje SQL de la API de DocumentDB para proporcionar una interfaz programable enriquecida a fin de hacer lógica condicional de procedimientos compleja con la ayuda de capacidades en tiempo real de JavaScript integradas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="6dcf2-578">SQL de la API de DocumentDB proporciona los argumentos a las UDF para cada uno de los documentos del origen en la fase actual (cláusulas WHERE o SELECT) de procesamiento de la UDF.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="6dcf2-579">El resultado se incorpora en el proceso de ejecución general perfectamente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="6dcf2-580">Si las propiedades a las que los parámetros UDF hacen referencia no están disponibles en el valor JSON, el parámetro se considera Undefined y así pues, la invocación de UDF se omite por completo.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="6dcf2-581">De forma similar, si el resultado de la UDF es Undefined, no se incluye en el resultado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="6dcf2-582">En resumen, las UDF son excelentes herramientas para hacer lógica de negocios como parte de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="6dcf2-583">Evaluación de operadores</span><span class="sxs-lookup"><span data-stu-id="6dcf2-583">Operator evaluation</span></span>
<span data-ttu-id="6dcf2-584">Cosmos DB, en virtud de ser una base de datos JSON, establece paralelismos con los operadores de JavaScript y su semántica de evaluación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="6dcf2-585">Aunque Cosmos DB intenta conservar la semántica de JavaScript en términos de soporte para JSON, la evaluación de operaciones se desvía en algunas instancias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="6dcf2-586">En SQL de la API de DocumentDB, a diferencia del lenguaje SQL tradicional, los tipos de valores no suelen conocerse hasta que los valores se recuperan de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="6dcf2-587">Para ejecutar consultas de forma eficaz, la mayoría de los operadores tienen requisitos de tipo estrictos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="6dcf2-588">SQL de la API de DocumentDB no realiza conversiones implícitas a diferencia de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="6dcf2-589">Por ejemplo, una consulta como `SELECT * FROM Person p WHERE p.Age = 21` coincide con documentos que contienen una propiedad Age cuyo valor es 21.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="6dcf2-590">Cualquier otro documento cuya propiedad Age coincida con la cadena "21", u otras variaciones posiblemente infinitas, como "021", "21,0", "0021", "00021", etc. no producirán coincidencias.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="6dcf2-591">Esto es en contraste al JavaScript donde los valores de cadena se convierten de manera implícita en números (en función del operador, por ejemplo, ==).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="6dcf2-592">Esta opción es fundamental para conseguir una coincidencia de índices eficaz en SQL de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="6dcf2-593">Consultas SQL con parámetros</span><span class="sxs-lookup"><span data-stu-id="6dcf2-593">Parameterized SQL queries</span></span>
<span data-ttu-id="6dcf2-594">Cosmos DB admite las consultas con parámetros que se expresen con la notación @ ya conocida.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="6dcf2-595">El uso de SQL con parámetros permite controlar y evitar de forma sólida la entrada por parte de los usuarios, impidiendo así la exposición accidental de datos a través de la inyección de código SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="6dcf2-596">Por ejemplo, puede escribir una consulta que acepte los apellidos y el estado de la dirección como parámetros y, a continuación, ejecutarla para distintos valores de los parámetros mencionados en función de la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="6dcf2-597">Después, esta solicitud puede enviarse a Cosmos DB como consulta JSON con parámetros, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="6dcf2-598">El argumento para TOP se puede definir mediante el uso de consultas con parámetros, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="6dcf2-599">Los valores de los parámetros pueden ser cualquier tipo de JSON válido (cadenas, números, booleanos, null o incluso matrices o JSON anidado).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="6dcf2-600">Además, como Cosmos DB no tiene ningún esquema, los parámetros no se validan respecto a ningún tipo.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="6dcf2-601"><a id="BuiltinFunctions"></a>Funciones integradas</span><span class="sxs-lookup"><span data-stu-id="6dcf2-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="6dcf2-602">Cosmos DB también admite un número de funciones integradas para operaciones comunes, que se pueden usar dentro de las consultas como funciones definidas por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="6dcf2-603">Grupo de funciones</span><span class="sxs-lookup"><span data-stu-id="6dcf2-603">Function group</span></span>          | <span data-ttu-id="6dcf2-604">Operaciones</span><span class="sxs-lookup"><span data-stu-id="6dcf2-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6dcf2-605">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="6dcf2-605">Mathematical functions</span></span>  | <span data-ttu-id="6dcf2-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN y TAN</span><span class="sxs-lookup"><span data-stu-id="6dcf2-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="6dcf2-607">Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-607">Type checking functions</span></span> | <span data-ttu-id="6dcf2-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="6dcf2-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="6dcf2-609">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="6dcf2-609">String functions</span></span>        | <span data-ttu-id="6dcf2-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING y UPPER</span><span class="sxs-lookup"><span data-stu-id="6dcf2-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="6dcf2-611">Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="6dcf2-611">Array functions</span></span>         | <span data-ttu-id="6dcf2-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH y ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="6dcf2-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="6dcf2-613">Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="6dcf2-613">Spatial functions</span></span>       | <span data-ttu-id="6dcf2-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID y ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="6dcf2-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="6dcf2-615">Si actualmente usa una función definida por el usuario (UDF) para la que ahora hay disponible una función integrada, debe usar la función integrada correspondiente ya que se va a ejecutar más rápidamente y va a ser más eficaz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="6dcf2-616">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="6dcf2-616">Mathematical functions</span></span>
<span data-ttu-id="6dcf2-617">Las funciones matemáticas realizan un cálculo, basado en valores de entrada proporcionados como argumentos, y devuelven un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="6dcf2-618">Esta es una tabla de las funciones matemáticas integradas admitidas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="6dcf2-619">Uso</span><span class="sxs-lookup"><span data-stu-id="6dcf2-619">Usage</span></span> | <span data-ttu-id="6dcf2-620">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcf2-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6dcf2-621">[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="6dcf2-622">Devuelve el valor absoluto (positivo) de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="6dcf2-624">Devuelve el valor entero más pequeño mayor o igual que la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="6dcf2-626">Devuelve el valor entero más grande menor o igual que la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="6dcf2-628">Devuelve el exponente de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="6dcf2-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="6dcf2-630">Devuelve el logaritmo natural de la expresión numérica especificada o bien el logaritmo que utiliza la base especificada</span><span class="sxs-lookup"><span data-stu-id="6dcf2-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="6dcf2-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="6dcf2-632">Devuelve el valor logarítmico de base 10 de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="6dcf2-634">Devuelve un valor numérico, redondeado al valor entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="6dcf2-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="6dcf2-636">Devuelve un valor numérico, truncado al valor entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="6dcf2-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="6dcf2-638">Devuelve la raíz cuadrada de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="6dcf2-640">Devuelve el cuadrado de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="6dcf2-642">Devuelve la potencia de la expresión numérica especificada al valor especificado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="6dcf2-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="6dcf2-644">Devuelve el valor de signo (-1, 0, 1) de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="6dcf2-646">Devuelve el ángulo, en radianes, cuyo coseno es la expresión numérica especificada; también se denomina arcocoseno.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="6dcf2-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="6dcf2-648">Devuelve el ángulo, en radianes, cuyo seno es la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="6dcf2-649">También se denomina arcoseno.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="6dcf2-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="6dcf2-651">Devuelve el ángulo, en radianes, cuya tangente es la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="6dcf2-652">También se denomina arcotangente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="6dcf2-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="6dcf2-654">Devuelve el ángulo, en radianes, entre el eje x positivo y el rayo desde el origen hasta el punto (y, x), donde x e y son los valores de las dos expresiones de punto flotante especificadas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="6dcf2-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="6dcf2-656">Devuelve el coseno trigonométrico del ángulo especificado, en radianes, en la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="6dcf2-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="6dcf2-658">Devuelve la cotangente trigonométrica del ángulo especificado, en radianes, en la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="6dcf2-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="6dcf2-660">Devuelve el ángulo correspondiente en grados de un ángulo especificado en radianes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="6dcf2-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="6dcf2-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="6dcf2-662">Devuelve el valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="6dcf2-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="6dcf2-664">Devuelve radianes cuando se especifica una expresión numérica en grados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="6dcf2-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="6dcf2-666">Devuelve el seno trigonométrico del ángulo especificado, en radianes, en la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="6dcf2-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="6dcf2-668">Devuelve la tangente de la expresión de entrada en la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="6dcf2-669">Por ejemplo, ya puede ejecutar consultas similares a las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="6dcf2-670">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="6dcf2-671">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-671">**Results**</span></span>

    [4]

<span data-ttu-id="6dcf2-672">La principal diferencia entre funciones de Cosmos DB y SQL ANSI es que están diseñadas para funcionar bien con datos sin esquemas y datos de esquemas mixtos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="6dcf2-673">Por ejemplo, si tiene un documento donde falta la propiedad de tamaño o tiene un valor no numérico, como "desconocido", se omite el documento, en lugar de devolver un error.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="6dcf2-674">Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-674">Type checking functions</span></span>
<span data-ttu-id="6dcf2-675">Las funciones de comprobación de tipos permiten comprobar el tipo de una expresión dentro de consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="6dcf2-676">Las funciones de comprobación de tipos pueden utilizarse para determinar el tipo de propiedades dentro de los documentos sobre la marcha cuando es variable o desconocido</span><span class="sxs-lookup"><span data-stu-id="6dcf2-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="6dcf2-677">Esta es una tabla de las funciones de comprobación de tipos integradas admitidas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="6dcf2-678"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="6dcf2-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="6dcf2-679"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="6dcf2-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-681">Devuelve un valor booleano que indica si el tipo del valor es una matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-683">Devuelve un valor booleano que indica si el tipo del valor es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-685">Devuelve un valor booleano que indica si el tipo del valor es nulo.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-687">Devuelve un valor booleano que indica si el tipo del valor es un número.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-689">Devuelve un valor booleano que indica si el tipo del valor es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-691">Devuelve un valor booleano que indica si el tipo del valor es una cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-693">Devuelve un valor booleano que indica si se ha asignado un valor a la propiedad.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="6dcf2-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="6dcf2-695">Devuelve un valor booleano que indica si el tipo del valor es una cadena, número, valor booleano o null.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="6dcf2-696">Con estas funciones, ya puede ejecutar consultas similares a las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="6dcf2-697">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="6dcf2-698">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="6dcf2-699">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="6dcf2-699">String functions</span></span>
<span data-ttu-id="6dcf2-700">Las siguientes funciones escalares realizan una operación sobre un valor de entrada de cadena y devuelven una cadena, un valor numérico o un booleano.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="6dcf2-701">A continuación se facilita una tabla de funciones de cadena integradas:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="6dcf2-702">Uso</span><span class="sxs-lookup"><span data-stu-id="6dcf2-702">Usage</span></span> | <span data-ttu-id="6dcf2-703">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcf2-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="6dcf2-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="6dcf2-705">Devuelve el número de caracteres de la expresión de cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="6dcf2-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="6dcf2-707">Devuelve una cadena que es el resultado de concatenar dos o más valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="6dcf2-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="6dcf2-709">Devuelve parte de una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="6dcf2-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="6dcf2-711">Devuelve un valor booleano que indica si la primera expresión de cadena finaliza con la segunda.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="6dcf2-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="6dcf2-713">Devuelve un valor booleano que indica si la primera expresión de cadena finaliza con la segunda.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="6dcf2-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="6dcf2-715">Devuelve un valor booleano que indica si la primera expresión de cadena contiene la segunda.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="6dcf2-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="6dcf2-717">Devuelve la posición inicial de la primera aparición de la expresión de la segunda cadena dentro de la primera expresión de cadena especificada, o -1 si no se encuentra la cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="6dcf2-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="6dcf2-719">Devuelve la parte izquierda de una cadena con el número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="6dcf2-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="6dcf2-721">Devuelve la parte derecha de una cadena con el número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="6dcf2-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="6dcf2-723">Devuelve una expresión de cadena después de quitar los espacios en blanco iniciales.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="6dcf2-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="6dcf2-725">Devuelve una expresión de cadena después de truncar todos los espacios en blanco finales.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="6dcf2-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="6dcf2-727">Devuelve una expresión de cadena después de convertir los datos de caracteres en mayúsculas a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="6dcf2-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="6dcf2-729">Devuelve una expresión de cadena después de convertir datos de caracteres en minúsculas a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="6dcf2-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="6dcf2-731">Reemplaza todas las apariciones de un valor de cadena especificado por otro valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="6dcf2-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="6dcf2-733">Repite un valor de cadena un número especificado de veces.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="6dcf2-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="6dcf2-735">Devuelve el orden inverso de un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="6dcf2-736">Con estas funciones, ya puede ejecutar consultas similares a las siguientes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="6dcf2-737">Por ejemplo, puede devolver el nombre de familia en mayúsculas del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="6dcf2-738">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="6dcf2-739">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="6dcf2-740">O concatenar cadenas como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="6dcf2-741">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="6dcf2-742">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="6dcf2-743">Las funciones de cadena también pueden usarse en la cláusula WHERE para filtrar los resultados, al igual que en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="6dcf2-744">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="6dcf2-745">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="6dcf2-746">Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="6dcf2-746">Array functions</span></span>
<span data-ttu-id="6dcf2-747">Las siguientes funciones escalares realizan una operación en un valor de entrada de matriz y devolver un valor numérico, booleano o de matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="6dcf2-748">A continuación se facilita una tabla de funciones de matriz integradas:</span><span class="sxs-lookup"><span data-stu-id="6dcf2-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="6dcf2-749">Uso</span><span class="sxs-lookup"><span data-stu-id="6dcf2-749">Usage</span></span> | <span data-ttu-id="6dcf2-750">Descripción</span><span class="sxs-lookup"><span data-stu-id="6dcf2-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="6dcf2-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="6dcf2-752">Devuelve el número de elementos de la expresión de matriz especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="6dcf2-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="6dcf2-754">Devuelve una matriz que es el resultado de concatenar dos o más valores de la matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="6dcf2-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="6dcf2-756">Devuelve un valor booleano que indica si la matriz contiene el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="6dcf2-757">Puede especificar si la coincidencia es completa o parcial.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="6dcf2-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="6dcf2-759">Devuelve parte de una expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="6dcf2-760">Las funciones de matriz pueden usarse para manipular matrices en JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="6dcf2-761">Por ejemplo, a continuación se facilita una consulta que devuelve todos los documentos en los que uno de los elementos primarios es "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="6dcf2-762">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="6dcf2-763">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="6dcf2-764">Puede especificar un fragmento parcial para los elementos que coinciden en la matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="6dcf2-765">La siguiente consulta busca todos los elementos primarios con el `givenName` de `Robin`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="6dcf2-766">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="6dcf2-767">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="6dcf2-768">Este es otro ejemplo que usa ARRAY_LENGTH para obtener el número de hijos por familia.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="6dcf2-769">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="6dcf2-770">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="6dcf2-771">Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="6dcf2-771">Spatial functions</span></span>
<span data-ttu-id="6dcf2-772">Cosmos DB admite las siguientes funciones integradas de Open Geospatial Consortium (OGC) para realizar consultas geoespaciales.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="6dcf2-773"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="6dcf2-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="6dcf2-774"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="6dcf2-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="6dcf2-776">Devuelve la distancia entre dos expresiones Point, Polygon o LineString de GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="6dcf2-778">Devuelve una expresión booleana que indica si el primer objeto de GeoJSON (Point, Polygon o LineString) está en el segundo objeto de GeoJSON (Point, Polygon o LineString).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="6dcf2-780">Devuelve una expresión booleana que indica si los dos objetos de GeoJSON especificados (Point, Polygon o LineString) intersecan.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="6dcf2-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="6dcf2-782">Devuelve un valor booleano que indica si la expresión de Point, Polygon o LineString de GeoJSON especificada es válida.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="6dcf2-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="6dcf2-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="6dcf2-784">Devuelve un valor JSON que contiene un valor booleano si la expresión de Point, Polygon o LineString de GeoJSON especificada es válida; si no es válida, devuelve también el motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="6dcf2-785">Las funciones espaciales pueden usarse para realizar consultas de proximidad con datos espaciales.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="6dcf2-786">Por ejemplo, aquí hay una consulta que devuelve todos los documentos de la familia que estén dentro de un radio de 30 km de la ubicación especificada mediante la función integrada ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="6dcf2-787">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="6dcf2-788">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="6dcf2-789">Para más información sobre la compatibilidad geoespacial en Cosmos DB, consulte [Uso de datos geoespaciales en Azure Cosmos DB](geospatial.md),</span><span class="sxs-lookup"><span data-stu-id="6dcf2-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="6dcf2-790">que contiene funciones espaciales y sintaxis de SQL para Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="6dcf2-791">Ahora veamos cómo funciona la consulta LINQ y cómo interactúa con la sintaxis que hemos visto hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="6dcf2-792"><a id="Linq"></a>LINQ para SQL de la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="6dcf2-793">LINQ es un modelo de programación de .NET que expresa cálculos como consultas de secuencias de objetos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="6dcf2-794">Cosmos DB proporciona una biblioteca del cliente para interactuar con LINQ facilitando una conversión entre objetos JSON y .NET, y una asignación a partir de un subconjunto de consultas de LINQ a consultas de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="6dcf2-795">En la imagen que se muestra a continuación vemos la arquitectura de consultas compatibles con LINQ que usa Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="6dcf2-796">Con el cliente de Cosmos DB, los desarrolladores pueden crear un objeto **IQueryable** que consulta directamente al proveedor de consultas de Cosmos DB que, a continuación, convierte la consulta de LINQ en una consulta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="6dcf2-797">La consulta pasa entonces al servidor de Cosmos DB para recuperar un conjunto de resultados en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="6dcf2-798">Los resultados devueltos se deserializan en una secuencia de objetos .NET en el cliente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Arquitectura de consultas compatibles con LINQ que usa la API de DocumentDB: sintaxis SQL, lenguaje de consulta JSON, conceptos de base de datos y consultas SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="6dcf2-800">Asignación de .NET y JSON</span><span class="sxs-lookup"><span data-stu-id="6dcf2-800">.NET and JSON mapping</span></span>
<span data-ttu-id="6dcf2-801">La asignación entre objetos .NET y documentos JSON es natural (cada campo del miembro de datos se asigna a un objeto JSON, donde el nombre del campo se asigna a la parte "clave" del objeto y la parte de "valor" se asigna de forma recursiva a la parte de valor del objeto.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="6dcf2-802">Considere el ejemplo siguiente: el objeto Family creado se asigna al documento JSON como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="6dcf2-803">Y viceversa, el documento JSON se reasigna de nuevo a un objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="6dcf2-804">**Clase de C#**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="6dcf2-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-to-sql-translation"></a><span data-ttu-id="6dcf2-806">LINQ para traducción de lenguaje SQL</span><span class="sxs-lookup"><span data-stu-id="6dcf2-806">LINQ to SQL translation</span></span>
<span data-ttu-id="6dcf2-807">El proveedor de consulta de Cosmos DB realiza una mejor opción de asignación desde una consulta de LINQ a una consulta SQL de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="6dcf2-808">En la siguiente descripción, asumimos la familiaridad básica del lector con LINQ.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="6dcf2-809">En primer lugar, para el sistema de tipos, admitimos todos los tipos primitivos JSON (tipos numéricos, booleanos, de cadena y null).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="6dcf2-810">Solo se admiten estos tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-810">Only these JSON types are supported.</span></span> <span data-ttu-id="6dcf2-811">Se admiten las siguientes expresiones escalares.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="6dcf2-812">Valores constantes: Entre estos se incluyen los valores constantes de los tipos de datos primitivos durante la evaluación de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="6dcf2-813">Expresiones de índice de propiedad o matriz: estas expresiones hacen referencia a la propiedad de un objeto o a un elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="6dcf2-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n es una variable int</span><span class="sxs-lookup"><span data-stu-id="6dcf2-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="6dcf2-815">Expresiones aritméticas: entre estas se incluyen expresiones aritméticas comunes o valores numéricos y booleanos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="6dcf2-816">Para ver la lista completa, consulte la especificación de SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="6dcf2-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="6dcf2-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="6dcf2-818">Expresión de comparación de cadenas: entre estas se incluye la comparación de un valor de cadena con algún valor de cadena constante.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="6dcf2-819">mother.familyName == "Smith";    child.givenName == s; //s es una variable de cadena</span><span class="sxs-lookup"><span data-stu-id="6dcf2-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="6dcf2-820">Expresión de creación de objetos o matrices: estas expresiones devuelven un objeto de tipo de valor compuesto o tipo anónimo o una matriz de estos objetos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="6dcf2-821">Estos valores se pueden anidar.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-821">These values can be nested.</span></span>
  
     <span data-ttu-id="6dcf2-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //un tipo anónimo con dos campos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="6dcf2-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="6dcf2-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="6dcf2-824"><a id="SupportedLinqOperators"></a>Lista de los operadores LINQ admitidos</span><span class="sxs-lookup"><span data-stu-id="6dcf2-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="6dcf2-825">La siguiente es una lista de los operadores LINQ admitidos en el proveedor LINQ incluido en el SDK de .NET de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="6dcf2-826">**Select**: Las proyecciones se traducen en la instrucción SQL SELECT, incluida la construcción de objetos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="6dcf2-827">**Where**: Los filtros se traducen a la instrucción SQL WHERE y admiten la traducción entre && , || y !</span><span class="sxs-lookup"><span data-stu-id="6dcf2-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="6dcf2-828">a los operadores SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-828">to the SQL operators</span></span>
* <span data-ttu-id="6dcf2-829">**SelectMany**: Permite desenredar las matrices a la cláusula SQL JOIN.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="6dcf2-830">Se puede usar para encadenar/anidar expresiones para filtrar los elementos de la matriz.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="6dcf2-831">**OrderBy y OrderByDescending**: Se traduce a ORDER BY ascendente/descendente</span><span class="sxs-lookup"><span data-stu-id="6dcf2-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="6dcf2-832">Los operadores **Count**, **Sum**, **Min**, **Max** y **Average** para la agregación y sus equivalentes asincrónicos **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** y **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="6dcf2-833">**CompareTo**: Se traduce a las comparaciones de intervalos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="6dcf2-834">Se usa frecuentemente para las cadenas, debido a que no son comparables en .NET.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="6dcf2-835">**Take**: Se traduce a la instrucción SQL TOP para limitar los resultados desde una consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="6dcf2-836">**Funciones matemáticas**: Admite la traducción desde Abs de .NET, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate a las funciones SQL integradas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="6dcf2-837">**Funciones de cadena**: Admite la traducción desde Concat .NET, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper a las funciones SQL integradas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="6dcf2-838">**Funciones de matriz**: Admite la traducción desde Concat .NET, Contains y Count a las funciones SQL integradas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="6dcf2-839">**Funciones de extensión geoespacial**: Admite la traducción desde los métodos auxiliares Distance, Within, IsValid y IsValidDetailed a las funciones SQL integradas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="6dcf2-840">**Función de extensión de función definida por el usuario**: Admite la traducción desde el método de código auxiliar UserDefinedFunctionProvider.Invoke a la correspondiente función definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="6dcf2-841">**Varios**: Admite la traducción de los operadores condicionales y de fusión.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="6dcf2-842">Puede traducir Contains a String CONTAINS, ARRAY_CONTAINS o SQL IN, según el contexto.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="6dcf2-843">Operadores de consulta SQL</span><span class="sxs-lookup"><span data-stu-id="6dcf2-843">SQL query operators</span></span>
<span data-ttu-id="6dcf2-844">A continuación, vemos algunos ejemplos que ilustran la traducción de algunos de los operadores de consulta de LINQ estándar a consultas de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="6dcf2-845">Operador Select</span><span class="sxs-lookup"><span data-stu-id="6dcf2-845">Select Operator</span></span>
<span data-ttu-id="6dcf2-846">La sintaxis es `input.Select(x => f(x))`, donde `f` es una expresión escalar.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="6dcf2-847">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="6dcf2-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="6dcf2-849">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="6dcf2-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="6dcf2-851">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="6dcf2-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="6dcf2-853">Operador SelectMany</span><span class="sxs-lookup"><span data-stu-id="6dcf2-853">SelectMany operator</span></span>
<span data-ttu-id="6dcf2-854">La sintaxis es `input.SelectMany(x => f(x))`, donde `f` es una expresión escalar que devuelve un tipo de colección.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="6dcf2-855">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="6dcf2-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="6dcf2-857">Operador Where</span><span class="sxs-lookup"><span data-stu-id="6dcf2-857">Where operator</span></span>
<span data-ttu-id="6dcf2-858">La sintaxis es `input.Where(x => f(x))`, donde `f` es una expresión escalar que devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="6dcf2-859">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="6dcf2-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="6dcf2-861">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="6dcf2-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="6dcf2-863">Composición de consultas SQL</span><span class="sxs-lookup"><span data-stu-id="6dcf2-863">Composite SQL queries</span></span>
<span data-ttu-id="6dcf2-864">Los operadores anteriores pueden ser compuestos para formar consultas más eficaces.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="6dcf2-865">Como Cosmos DB admite recopilaciones anidadas, la composición puede concatenarse o anidarse.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="6dcf2-866">Concatenación</span><span class="sxs-lookup"><span data-stu-id="6dcf2-866">Concatenation</span></span>
<span data-ttu-id="6dcf2-867">La sintaxis es `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="6dcf2-868">Una consulta concatenada puede empezar por una consulta `SelectMany` opcional seguida de varios operadores `Select` o `Where`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="6dcf2-869">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="6dcf2-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="6dcf2-871">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="6dcf2-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="6dcf2-873">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="6dcf2-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="6dcf2-875">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="6dcf2-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="6dcf2-877">Anidamiento</span><span class="sxs-lookup"><span data-stu-id="6dcf2-877">Nesting</span></span>
<span data-ttu-id="6dcf2-878">La sintaxis es `input.SelectMany(x=>x.Q())`, donde Q es un operador `Select`, `SelectMany` o `Where`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="6dcf2-879">En una consulta anidada, la consulta interna se aplica a cada uno de los elementos de la recopilación externa.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="6dcf2-880">Una característica importante es que la consulta interna puede hacer referencia a los campos de los elementos de la recopilación externa como las autocombinaciones.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="6dcf2-881">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="6dcf2-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="6dcf2-883">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="6dcf2-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="6dcf2-885">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="6dcf2-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="6dcf2-887"><a id="ExecutingSqlQueries"></a>Ejecución de consultas SQL</span><span class="sxs-lookup"><span data-stu-id="6dcf2-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="6dcf2-888">Cosmos DB expone recursos mediante la API de REST, que puede invocar cualquier lenguaje capaz de realizar solicitudes de HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="6dcf2-889">Además, Cosmos DB ofrece bibliotecas de programación para varios lenguajes populares como .NET, Node.js, JavaScript y Python.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="6dcf2-890">La API de REST y las diversas bibliotecas admiten la realización de consultas a través de SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="6dcf2-891">El SDK de .NET admite la realización de consultas de LINQ, además del lenguaje SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="6dcf2-892">En los ejemplos siguientes se muestra cómo crear una consulta y enviarla a una cuenta de la base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="6dcf2-893"><a id="RestAPI"></a>API DE REST</span><span class="sxs-lookup"><span data-stu-id="6dcf2-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="6dcf2-894">Cosmos DB ofrece un modelo de programación RESTful sobre HTTP.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="6dcf2-895">Las cuentas de la base de datos pueden aprovisionarse usando una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="6dcf2-896">El modelo de recursos de Cosmos DB consta de un conjunto de recursos en una cuenta de base de datos, cada uno de los cuales se puede dirigir mediante un URI lógico y estable.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="6dcf2-897">En este documento, se hace referencia a un conjunto de recursos como fuente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="6dcf2-898">Una cuenta de la base de datos consta de un conjunto de bases de datos, cada una incluyendo varias recopilaciones que, a su vez, contienen documentos, UDF y otros tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="6dcf2-899">El modelo de interacción básico con estos recursos se lleva a cabo a través de los verbos GET, PUT, POST y DELETE de HTTP con su interpretación estándar.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="6dcf2-900">El verbo POST se usa para la creación de un nuevo recurso, para ejecutar un procedimiento almacenado o para emitir una consulta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="6dcf2-901">Las consultas siempre son operaciones de solo lectura sin efectos secundarios.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="6dcf2-902">En los ejemplos siguientes se muestra una operación POST para una consulta de la API de DocumentDB realizada en una colección que incluye los dos documentos de ejemplo que hemos revisado hasta el momento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="6dcf2-903">La consulta tiene un filtro sencillo por la propiedad de nombre JSON.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="6dcf2-904">Fíjese en el uso de los encabezados `x-ms-documentdb-isquery` y Content-Type: `application/query+json` para denotar que la operación es una consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="6dcf2-905">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="6dcf2-906">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="6dcf2-907">En el segundo ejemplo se muestra una consulta más compleja que devuelve varios resultados de la combinación.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="6dcf2-908">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="6dcf2-909">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="6dcf2-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="6dcf2-910">Si los resultados de una consulta no caben en una sola página, la API de REST devuelve un token de continuación a través del encabezado de respuesta `x-ms-continuation-token` .</span><span class="sxs-lookup"><span data-stu-id="6dcf2-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="6dcf2-911">Los clientes pueden paginar los resultados incluyendo el encabezado en resultados posteriores.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="6dcf2-912">El número de resultados por página también se puede controlar a través del encabezado numérico `x-ms-max-item-count` .</span><span class="sxs-lookup"><span data-stu-id="6dcf2-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="6dcf2-913">Si la consulta especificada tiene una función de agregación como `COUNT`, la página de consulta puede devolver un valor parcialmente agregado sobre la página de resultados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="6dcf2-914">Los clientes deben realizar una agregación de segundo nivel con estos resultados para generar los resultados finales, por ejemplo, sumar los recuentos devueltos en las páginas individuales para devolver el recuento total.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="6dcf2-915">Para administrar la directiva de coherencia de datos para consultas, use el encabezado `x-ms-consistency-level` como todas las solicitudes de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="6dcf2-916">Para que la sesión sea coherente, también es necesario enviar el último encabezado de cookie `x-ms-session-token` en la solicitud de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="6dcf2-917">La directiva de indexación de la colección consultada también puede afectar a la coherencia de los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="6dcf2-918">En el caso de las recopilaciones, con la configuración de la directiva de indexación predeterminada, el índice siempre está actualizado con el contenido del documento y los resultados de la consulta coinciden con la coherencia elegida para los datos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="6dcf2-919">Si la directiva de índices se suaviza para los perezosos, las consultas pueden devolver resultados obsoletos.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="6dcf2-920">Para más información, vea [Niveles de coherencia en Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="6dcf2-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="6dcf2-921">Si la directiva de índices configurada de la recopilación no puede admitir la consulta especificada, el servidor de Azure Cosmos DB devuelve el error 400 de "solicitud incorrecta".</span><span class="sxs-lookup"><span data-stu-id="6dcf2-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="6dcf2-922">Esto se devuelve para las consultas por rango en rutas de acceso configuradas para búsquedas hash (igualdad) y rutas de acceso excluidas de forma explícita de los índices.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="6dcf2-923">Se puede especificar el encabezado `x-ms-documentdb-query-enable-scan` para permitir que la consulta realice un examen si algún índice no está disponible.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="6dcf2-924">Puede obtener métricas detalladas sobre la ejecución de consultas si establece el encabezado `x-ms-documentdb-populatequerymetrics` en `True`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="6dcf2-925">Para más información, vea, [Métricas de consulta de SQL para la API de DocumentDB de Azure Cosmos DB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6dcf2-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="6dcf2-926"><a id="DotNetSdk"></a>SDK de C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="6dcf2-927">El SDK de .NET admite la realización de consultas de LINQ y SQL.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="6dcf2-928">En el ejemplo siguiente se muestra cómo realizar la consulta de filtro simple incluida anteriormente en este documento.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="6dcf2-929">En este ejemplo se comparan dos propiedades para igualdad en cada documento y se usan proyecciones anónimas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="6dcf2-930">En el ejemplo siguiente se muestran combinaciones, expresadas a través de SelectMany de LINQ.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="6dcf2-931">El cliente de .NET se itera automáticamente a través de todas las páginas de resultados de la consulta de los bloques foreach, como se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="6dcf2-932">Las opciones de consulta especificadas en la sección de la API de REST también están disponibles en el SDK de .NET mediante las clases `FeedOptions` and `FeedResponse` del método CreateDocumentQuery.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="6dcf2-933">El número de páginas se puede controlar con el valor `MaxItemCount` .</span><span class="sxs-lookup"><span data-stu-id="6dcf2-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="6dcf2-934">Puede controlar expresamente la paginación creando `IDocumentQueryable` mediante el objeto `IQueryable`; después, leyendo los` ResponseContinuationToken` valores y devolviéndolos como `RequestContinuationToken` en `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="6dcf2-935">`EnableScanInQuery` para habilitar los exámenes cuando la directiva de indexación configurada no pueda admitir la consulta.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="6dcf2-936">Para las colecciones con particiones, puede usar `PartitionKey` para ejecutar la consulta en una sola partición (aunque Cosmos DB puede extraer automáticamente esto a partir del texto de consulta), y `EnableCrossPartitionQuery` para ejecutar consultas que se deben ejecutar en varias particiones.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="6dcf2-937">Consulte los [ejemplos de .NET de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) para obtener más casos que contengan consultas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="6dcf2-938"><a id="JavaScriptServerSideApi"></a>API del servidor de JavaScript</span><span class="sxs-lookup"><span data-stu-id="6dcf2-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="6dcf2-939">Cosmos DB proporciona un modelo de programación para ejecutar una lógica de aplicación basada en JavaScript directamente en las recopilaciones usando procedimientos y desencadenadores almacenados.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="6dcf2-940">La lógica de JavaScript registrada en un nivel de recopilación puede emitir operaciones de base de datos en las operaciones de los documentos de la recopilación especificada.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="6dcf2-941">Estas operaciones se incluyen en transacciones ACID ambientales.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="6dcf2-942">En el ejemplo siguiente se muestra cómo usar queryDocuments en la API del servidor de JavaScript para realizar consultas a partir de procedimientos y desencadenadores almacenados dentro.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="6dcf2-943"><a id="References"></a>Referencias</span><span class="sxs-lookup"><span data-stu-id="6dcf2-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="6dcf2-944">[Introducción a Azure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="6dcf2-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="6dcf2-945">Especificación de SQL de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="6dcf2-946">Ejemplos de .NET de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6dcf2-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="6dcf2-947">[Niveles de coherencia de Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="6dcf2-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="6dcf2-948">SQL ANSI 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="6dcf2-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="6dcf2-950">Especificación de JavaScript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="6dcf2-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="6dcf2-952">Técnicas de evaluación de consultas para bases de datos de gran tamaño [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="6dcf2-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="6dcf2-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="6dcf2-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="6dcf2-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="6dcf2-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="6dcf2-956">G.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-956">G.</span></span> <span data-ttu-id="6dcf2-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-957">Graefe.</span></span> <span data-ttu-id="6dcf2-958">El marco de cascadas para la optimización de consultas.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="6dcf2-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-959">IEEE Data Eng.</span></span> <span data-ttu-id="6dcf2-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="6dcf2-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md