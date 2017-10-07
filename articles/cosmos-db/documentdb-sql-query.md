---
title: consultas de aaaSQL para la API de documentos de base de datos de Azure Cosmos | Documentos de Microsoft
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
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="fb4bf-105">Consultas SQL para la API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb4bf-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="fb4bf-106">Microsoft Azure Cosmos DB admite la consulta de documentos con SQL (lenguaje de consulta estructurado) como lenguaje de consulta de JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="fb4bf-107">Cosmos DB realmente no tiene esquemas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="fb4bf-108">En virtud de su compromiso toohello JSON modelo de datos directamente en el motor de base de datos de hello, proporciona la indexación automática de documentos JSON sin necesidad de esquema explícito o la creación de índices secundarios.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="fb4bf-109">Al diseñar el lenguaje de consulta de Hola para Cosmos DB, hemos tenido en cuenta dos objetivos:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="fb4bf-110">En lugar de crear un nuevo lenguaje de consulta JSON, deseamos toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="fb4bf-111">SQL es uno de los lenguajes de consulta de hello más familiares y conocidos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="fb4bf-112">SQL de Cosmos DB proporciona un modelo de programación formal para consultas enriquecidas en documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="fb4bf-113">Como JSON documento base de datos puede ejecutar JavaScript directamente en el motor de base de datos de hello, deseamos modelo de programación de JavaScript de toouse como base de hello para el lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="fb4bf-114">Hola documentos API SQL se basa en el sistema de tipos de JavaScript, la evaluación de expresiones y la invocación de función.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="fb4bf-115">A su vez, esto proporciona un modelo de programación natural para proyecciones relacionales, navegación jerárquica por documentos JSON, autocombinaciones, consultas espaciales e invocación de funciones definidas por el usuario (UDF) escritas íntegramente en JavaScript, entre otras características.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="fb4bf-116">Creemos que estas capacidades son fricción de hello tooreducing clave entre la aplicación hello y base de datos de Hola y son cruciales para la productividad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="fb4bf-117">Se recomienda introducción, inspeccionando Hola después de vídeo, donde Aravind Ramachandran muestra las capacidades de creación de consultas de Cosmos DB y al visitar nuestro [Query Playground](http://www.documentdb.com/sql/demo), donde puede probar DB Cosmos y ejecutar consultas SQL en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="fb4bf-118">A continuación, devolver toothis artículo, donde se comienza con un tutorial de consulta SQL que le guiará por algunos documentos sencillos de JSON y los comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="fb4bf-119"><a id="GettingStarted"></a>Introducción a los comandos SQL en Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb4bf-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="fb4bf-120">toosee Cosmos base de datos SQL en trabajar, vamos a empezar con algunos documentos JSON simples y guiar algunas consultas sencillas con ella.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="fb4bf-121">Tenga en cuenta estos dos documentos JSON sobre dos familias.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="fb4bf-122">Con la base de datos de Cosmos, no necesitamos toocreate los esquemas o los índices secundarios explícitamente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="fb4bf-123">Se simplemente necesita tooinsert Hola JSON documentos tooa colección DB Cosmos y posteriormente realiza una consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="fb4bf-124">Aquí tenemos un simple del JSON documentos para hello familia Andersen, Hola principales, los elementos secundarios (y sus mascotas), dirección e información de registro.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="fb4bf-125">documento de Hello tiene cadenas, números, valores booleanos, matrices y las propiedades anidadas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="fb4bf-126">**Documento**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-126">**Document**</span></span>  

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

<span data-ttu-id="fb4bf-127">Aquí se muestra un segundo documento con una sutil diferencia: se usan `givenName` y `familyName` en lugar de `firstName` y `lastName`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="fb4bf-128">**Documento**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-128">**Document**</span></span>  

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

<span data-ttu-id="fb4bf-129">Ahora vamos a intentarlo algunas consultas contra este toounderstand datos algunos Hola los aspectos clave de SQL de la API de documentos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="fb4bf-130">Por ejemplo, siguiente Hola consulta devuelve documentos de Hola que coincide con el campo de Id. de hello `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="fb4bf-131">Puesto que es un `SELECT *`, resultado de hello de consulta de hello es documento JSON de hello completo:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="fb4bf-132">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-133">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-133">**Results**</span></span>

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


<span data-ttu-id="fb4bf-134">Ahora considere la posibilidad de caso de Hola que necesitamos tooreformat Hola salida JSON en una forma diferente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="fb4bf-135">Esta consulta proyectos JSON nuevo objeto con dos campos seleccionados, Name y City, cuando ciudad de la dirección hello tiene Hola mismo nombre como estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="fb4bf-136">En este caso, "NY, NY" coincide.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="fb4bf-137">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="fb4bf-138">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="fb4bf-139">consulta siguiente de Hello devuelve todos los nombres especificados de Hola de elementos secundarios de familia de hello cuyo identificador coincide con `WakefieldFamily` ordenadas por ciudad Hola de residencia.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="fb4bf-140">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="fb4bf-141">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="fb4bf-142">Nos gustaría toodraw atención tooa algunos aspectos importantes de hello Cosmos DB consultar lenguaje a través de ejemplos de Hola que hemos visto hasta ahora:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="fb4bf-143">Como SQL de la API de DocumentDB funciona con valores JSON, trata entidades en forma de árbol en lugar de filas y columnas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="fb4bf-144">Por lo tanto, el lenguaje de hello le permite hacer referencia toonodes del árbol de Hola en cualquier profundidad arbitraria, como `Node1.Node2.Node3…..Nodem`, similar toorelational SQL que hace referencia toohello dos referencia de una parte de `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="fb4bf-145">Hola estructurado funciona de lenguaje de consulta con los datos sin esquema.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="fb4bf-146">Por lo tanto, Hola tipo sistema necesidades toobe enlazados dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="fb4bf-147">Hello misma expresión puede producir distintos tipos en los distintos documentos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="fb4bf-148">resultado de Hello de una consulta es un valor JSON válido, pero no se garantiza que toobe de un esquema fijo.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="fb4bf-149">Cosmos DB solo admite documentos JSON estrictos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="fb4bf-150">Esto significa expresiones y sistema de tipos de hello son toodeal restringida solo con los tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="fb4bf-151">Consulte toohello [especificación de JSON](http://www.json.org/) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="fb4bf-152">Una recopilación de Cosmos DB es un contenedor sin esquemas de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="fb4bf-153">relaciones de Hello en entidades de datos dentro y entre documentos en una colección implícitamente se capturan de contención y no primary key y relaciones de clave externas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="fb4bf-154">Se trata de un aspecto importante que vale la pena señalar a la luz de combinaciones de hello dentro de los documentos que se describe más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="fb4bf-155"><a id="Indexing"></a> Indexación de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb4bf-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="fb4bf-156">Antes de entrar en hello sintaxis SQL de la API de documentos, merece la pena explorar Hola indización de diseño en la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="fb4bf-157">Hola de índices de la base de datos sirve tooserve consultas en sus diversas formas y formas con el consumo de recursos mínimo (por ejemplo, CPU y de entrada/salida) al proporcionar un buen rendimiento y latencia baja.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="fb4bf-158">A menudo, elección de Hola de índice correcto de Hola para consultar una base de datos requiere mucho planeamiento y la experimentación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="fb4bf-159">Este enfoque supone un desafío para las bases de datos sin esquema en los datos de hello tooa estricta del esquema no es conforme y evoluciona rápidamente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="fb4bf-160">Por lo tanto, cuando se diseñó el subsistema de indización de base de datos de Cosmos hello, establecemos Hola siguientes objetivos:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="fb4bf-161">Indizar los documentos sin necesidad de esquema: Hola indización subsistema no requiere ninguna información de esquema ni realizar ninguna suposición acerca del esquema de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="fb4bf-162">Compatibilidad con gran y eficaz consultas relacionales y jerárquicas: el índice Hola admite lenguaje de consulta de base de datos de Cosmos Hola eficazmente, incluida la compatibilidad para las proyecciones relacionales y jerárquicas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="fb4bf-163">Compatibilidad con las consultas coherente en caso de un volumen sostenido de escrituras: escritura alto rendimiento las cargas de trabajo con consultas coherente, Hola índice se actualiza incrementalmente, eficaz y en línea en cara Hola de un volumen sostenido de escrituras.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="fb4bf-164">actualización de índice coherente de Hello es fundamental tooserve consultas de hello en el nivel de coherencia de hello en qué servicio de documento Hola Hola de configurada por el usuario.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="fb4bf-165">Compatibilidad con la arquitectura multiempresa: dado el modelo de basadas en reservas de hello para la regulación de recursos entre los inquilinos, se realizan las actualizaciones del índice dentro del presupuesto Hola de recursos del sistema (CPU, memoria y operaciones de entrada/salida por segundo) asignadas por la réplica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="fb4bf-166">Eficacia de almacenamiento: para obtener rentabilidad, almacenamiento sobrecarga de hello en el disco del índice de hello es limitada y de predicción.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="fb4bf-167">Esto es fundamental porque Cosmos DB permite Hola developer toomake basado en costos contrapartidas sobrecarga de índice en el rendimiento de las consultas toohello relación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="fb4bf-168">Consulte toohello [ejemplos de base de datos de Azure Cosmos](https://github.com/Azure/azure-documentdb-net) en MSDN para ejemplos que muestran cómo tooconfigure Hola directiva de indexación de una colección.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="fb4bf-169">Supongamos ahora entraremos en detalles de Hola de hello sintaxis SQL de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="fb4bf-170"><a id="Basics"></a>Conceptos básicos de una consulta SQL de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb4bf-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="fb4bf-171">Todas las consultas constan de una cláusula SELECT y cláusulas FROM y WHERE opcionales por estándares ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="fb4bf-172">Por lo general, para cada consulta, se enumera el origen de hello en la cláusula FROM de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="fb4bf-173">A continuación, Hola filtrar Hola de cláusula WHERE se aplica en hello origen tooretrieve un subconjunto de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="fb4bf-174">Por último, se utiliza la cláusula SELECT Hola Hola tooproject solicitado valores JSON en hello seleccione lista.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="fb4bf-175"><a id="FromClause"></a>Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="fb4bf-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="fb4bf-176">Hola `FROM <from_specification>` cláusula es opcional, a menos que se filtra o proyecta más adelante en la consulta de hello origen Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="fb4bf-177">Hola de esta cláusula sirve toospecify origen de datos de hello en qué Hola debe funcionar la consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="fb4bf-178">Normalmente recolección completa de hello es origen hello, pero uno en su lugar, puede especificar un subconjunto del conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="fb4bf-179">Al igual que una consulta `SELECT * FROM Families` indica que la colección completa de las familias de hello es origen Hola sobre qué tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="fb4bf-180">Un identificador especial raíz puede ser usado toorepresent Hola colección en lugar de usar el nombre de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="fb4bf-181">Hello lista siguiente contiene reglas de Hola que se aplican por cada consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="fb4bf-182">colección de Hello puede tener alias, como `SELECT f.id FROM Families AS f` o simplemente `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="fb4bf-183">Aquí `f` es equivalente a hello `Families`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="fb4bf-184">`AS`es un identificador de palabra clave opcional tooalias Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="fb4bf-185">Una vez tiene un alias, no se puede enlazar el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="fb4bf-186">Por ejemplo, `SELECT Families.id FROM Families f` es sintácticamente válida porque no se puede resolver el identificador de Hola "Familias" ya.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="fb4bf-187">Todas las propiedades que deben toobe al que hace referencia deben ser nombres completos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="fb4bf-188">En ausencia de Hola de adherencia estricta del esquema, se trata de tooavoid ha aplicado los enlaces ambiguos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="fb4bf-189">Por lo tanto, `SELECT id FROM Families f` es sintácticamente válida desde la propiedad de hello `id` no está enlazado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="fb4bf-190">Subdocumentos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-190">Subdocuments</span></span>
<span data-ttu-id="fb4bf-191">origen de Hello también puede ser el subconjunto más pequeño de tooa reducida.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="fb4bf-192">Por ejemplo, tooenumerating sólo un subárbol en cada documento, subroot Hola se convertiría en origen hello, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="fb4bf-193">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="fb4bf-194">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-194">**Results**</span></span>  

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

<span data-ttu-id="fb4bf-195">Mientras Hola anteriormente en el ejemplo utiliza una matriz como origen de hello, un objeto también podría usarse como origen de hello, que es lo que se muestra en el siguiente ejemplo de Hola: cualquier valor JSON válido (no definido) que se pueden encontrar en el origen de Hola se considera para su inclusión en el resultado de hello de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="fb4bf-196">Si no dispone de algunas familias un `address.state` valor, se excluyen Hola del resultado de consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="fb4bf-197">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="fb4bf-198">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="fb4bf-199"><a id="WhereClause"></a>Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="fb4bf-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="fb4bf-200">Hola de cláusula WHERE (**`WHERE <filter_condition>`**) es opcional.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="fb4bf-201">Especifica Hola condiciones que deben satisfacer los documentos JSON de hello proporcionadas por el origen de hello en toobe orden incluido como parte del resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="fb4bf-202">Se debe evaluar cualquier documento JSON Hola especifica condiciones demasiado "true" toobe tienen en cuenta para el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="fb4bf-203">Hola donde se utiliza la cláusula por nivel de índice de hello en orden toodetermine Hola absoluta subconjunto más pequeño de documentos de origen que pueden ser parte del resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="fb4bf-204">Hello consulta siguiente solicita los documentos que contienen una propiedad de nombre cuyo valor es `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="fb4bf-205">Cualquier otro documento que no tiene una propiedad name, o donde no coincide con el valor de Hola `AndersenFamily` se excluye.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="fb4bf-206">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-207">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="fb4bf-208">ejemplo de Hola anterior mostró una consulta de igualdad simple.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="fb4bf-209">SQL de la API de DocumentDB también admite diversas expresiones escalares.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="fb4bf-210">Hola más utilizado son expresiones unarios y binarios.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="fb4bf-211">Las referencias de propiedad desde un objeto JSON origen hello también son expresiones válidas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="fb4bf-212">Hola después de los operadores binarios es compatibles actualmente y puede utilizarse en consultas, como se muestra en hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="fb4bf-213">Aritméticos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="fb4bf-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="fb4bf-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fb4bf-215">Bit a bit</span><span class="sxs-lookup"><span data-stu-id="fb4bf-215">Bitwise</span></span></td>    
<td><span data-ttu-id="fb4bf-216">|, &, ^, <<, >>, >>> (desplazamiento a la derecha con relleno de ceros)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fb4bf-217">Lógicos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-217">Logical</span></span></td>
<td><span data-ttu-id="fb4bf-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="fb4bf-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fb4bf-219">De comparación</span><span class="sxs-lookup"><span data-stu-id="fb4bf-219">Comparison</span></span></td>    
<td><span data-ttu-id="fb4bf-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="fb4bf-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fb4bf-221">Cadena</span><span class="sxs-lookup"><span data-stu-id="fb4bf-221">String</span></span></td>    
<td><span data-ttu-id="fb4bf-222">|| (concatenar)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="fb4bf-223">Echemos un vistazo a algunas consultas usando operadores binarios.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="fb4bf-224">Hola operadores unarios +,-, ~ también son compatibles y no puede utilizarse dentro de consultas, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="fb4bf-225">Además toobinary y los operadores unarios, referencias de propiedad también se permiten.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="fb4bf-226">Por ejemplo, `SELECT * FROM Families f WHERE f.isRegistered` devuelve Hola documento JSON que contiene la propiedad de hello `isRegistered` donde el valor de la propiedad de hello es igual toohello JSON `true` valor.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="fb4bf-227">Cualquier otro valor (false, null, sin definir, `<number>`, `<string>`, `<object>`, `<array>`, etc.) lleva toohello documento de origen se excluye del resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="fb4bf-228">Operadores de igualdad y de comparación</span><span class="sxs-lookup"><span data-stu-id="fb4bf-228">Equality and comparison operators</span></span>
<span data-ttu-id="fb4bf-229">Hello siguiente tabla muestra hello resultado de las comparaciones de igualdad en SQL de la API de documentos entre los dos tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-233">
            <strong>Booleano</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-234">
            <strong>Número</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-235">
            <strong>Cadena</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-236">
            <strong>Objeto</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fb4bf-237">
            <strong>Matriz</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fb4bf-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-254">
            <strong>Booleano<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fb4bf-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-262">
            <strong>Número<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fb4bf-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-270">
            <strong>Cadena<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fb4bf-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-278">
            <strong>Objeto<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fb4bf-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fb4bf-286">
            <strong>Matriz<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fb4bf-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fb4bf-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fb4bf-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fb4bf-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="fb4bf-294">Para otros operadores de comparación como >, > =,! =, < y < =, hello se aplican las reglas siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="fb4bf-295">La comparación entre los tipos da lugar a Undefined.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="fb4bf-296">La comparación entre dos objetos o dos matrices da lugar a Undefined.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="fb4bf-297">Si el resultado de hello de expresión escalar de hello en el filtro de hello es sin definir, documento correspondiente hello no se incluiría en el resultado de hello, ya que Undefined lógicamente no equipare demasiado "true".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="fb4bf-298">Palabra clave BETWEEN</span><span class="sxs-lookup"><span data-stu-id="fb4bf-298">BETWEEN keyword</span></span>
<span data-ttu-id="fb4bf-299">También puede utilizar consultas de tooexpress de hello BETWEEN palabra clave en intervalos de valores como en ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="fb4bf-300">BETWEEN puede utilizarse con cadenas o números.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="fb4bf-301">Por ejemplo, esta consulta devuelve todos los documentos familias en qué Hola grado del primer nodo secundario está entre 1-5 (ambos inclusive).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="fb4bf-302">A diferencia de en ANSI-SQL, se puede utilizar también Hola BETWEEN cláusula en la cláusula FROM de hello como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="fb4bf-303">Para los tiempos de ejecución de consulta más rápidos, recuerde toocreate una directiva de indexación que usa un tipo de índice de intervalo con las propiedades/rutas numéricas que se filtran en la cláusula de hello BETWEEN.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="fb4bf-304">Hola principal diferencia entre utilizar BETWEEN en API de documentos y ANSI SQL es que se pueden expresar consultas por rango en Propiedades de tipos mixtos, por ejemplo, podría tener que "grado" ser un número (5) en algunos documentos y cadenas en otros ("grade4").</span><span class="sxs-lookup"><span data-stu-id="fb4bf-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="fb4bf-305">En estos casos, al igual que en JavaScript, una comparación entre dos resultados de diferentes tipos en "undefined" y documento de Hola se omitirán.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="fb4bf-306">Operadores lógicos (Y, O y NO)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="fb4bf-307">Los operadores lógicos operan en valores booleanos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="fb4bf-308">Hola tablas lógicas de verdad para estos operadores se muestran en hello las tablas siguientes.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="fb4bf-309">OR</span><span class="sxs-lookup"><span data-stu-id="fb4bf-309">OR</span></span> | <span data-ttu-id="fb4bf-310">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-310">True</span></span> | <span data-ttu-id="fb4bf-311">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-311">False</span></span> | <span data-ttu-id="fb4bf-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fb4bf-313">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-313">True</span></span> |<span data-ttu-id="fb4bf-314">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-314">True</span></span> |<span data-ttu-id="fb4bf-315">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-315">True</span></span> |<span data-ttu-id="fb4bf-316">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-316">True</span></span> |
| <span data-ttu-id="fb4bf-317">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-317">False</span></span> |<span data-ttu-id="fb4bf-318">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-318">True</span></span> |<span data-ttu-id="fb4bf-319">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-319">False</span></span> |<span data-ttu-id="fb4bf-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-320">Undefined</span></span> |
| <span data-ttu-id="fb4bf-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-321">Undefined</span></span> |<span data-ttu-id="fb4bf-322">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-322">True</span></span> |<span data-ttu-id="fb4bf-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-323">Undefined</span></span> |<span data-ttu-id="fb4bf-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-324">Undefined</span></span> |

| <span data-ttu-id="fb4bf-325">Y</span><span class="sxs-lookup"><span data-stu-id="fb4bf-325">AND</span></span> | <span data-ttu-id="fb4bf-326">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-326">True</span></span> | <span data-ttu-id="fb4bf-327">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-327">False</span></span> | <span data-ttu-id="fb4bf-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fb4bf-329">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-329">True</span></span> |<span data-ttu-id="fb4bf-330">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-330">True</span></span> |<span data-ttu-id="fb4bf-331">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-331">False</span></span> |<span data-ttu-id="fb4bf-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-332">Undefined</span></span> |
| <span data-ttu-id="fb4bf-333">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-333">False</span></span> |<span data-ttu-id="fb4bf-334">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-334">False</span></span> |<span data-ttu-id="fb4bf-335">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-335">False</span></span> |<span data-ttu-id="fb4bf-336">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-336">False</span></span> |
| <span data-ttu-id="fb4bf-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-337">Undefined</span></span> |<span data-ttu-id="fb4bf-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-338">Undefined</span></span> |<span data-ttu-id="fb4bf-339">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-339">False</span></span> |<span data-ttu-id="fb4bf-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-340">Undefined</span></span> |

| <span data-ttu-id="fb4bf-341">NO</span><span class="sxs-lookup"><span data-stu-id="fb4bf-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="fb4bf-342">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-342">True</span></span> |<span data-ttu-id="fb4bf-343">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-343">False</span></span> |
| <span data-ttu-id="fb4bf-344">False</span><span class="sxs-lookup"><span data-stu-id="fb4bf-344">False</span></span> |<span data-ttu-id="fb4bf-345">True</span><span class="sxs-lookup"><span data-stu-id="fb4bf-345">True</span></span> |
| <span data-ttu-id="fb4bf-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-346">Undefined</span></span> |<span data-ttu-id="fb4bf-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="fb4bf-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="fb4bf-348">Palabra clave IN</span><span class="sxs-lookup"><span data-stu-id="fb4bf-348">IN keyword</span></span>
<span data-ttu-id="fb4bf-349">palabra clave IN de Hello puede ser usado toocheck si un valor especificado coincide con algún valor en una lista.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="fb4bf-350">Por ejemplo, esta consulta devuelve todos los documentos familias donde Id. de hello es uno de "WakefieldFamily" o "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="fb4bf-351">Este ejemplo devuelve todos los documentos donde el estado de hello es uno de hello especificado valores.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="fb4bf-352">Operadores ternario (?) y de fusión (??)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="fb4bf-353">operadores de ternario y Coalesce de Hello pueden ser expresiones condicionales toobuild usado, toopopular similar programación lenguajes como C# y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="fb4bf-354">operador ternario (?) de Hello puede ser muy útil cuando la creación de nuevas propiedades JSON en hello volar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="fb4bf-355">Por ejemplo, ahora puede escribir niveles de clase de consultas tooclassify hello en un formato legible humano como principiante/intermedio/Advanced tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="fb4bf-356">También puede anidar Hola llamadas toohello (operador) como en la siguiente consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="fb4bf-357">Como con otros operadores de consulta, si hello que se hace referencia en una expresión condicional Hola faltan propiedades en cualquier documento, si los tipos de Hola que se comparan son diferentes, a continuación, esos documentos se excluyen o en resultados de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="fb4bf-358">Hello Coalesce (?) puede ser usa tooefficiently comprobación presencia de Hola de una propiedad (conocido como)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="fb4bf-359">(es decir, si esta se ha definido) en un documento.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-359">is defined) in a document.</span></span> <span data-ttu-id="fb4bf-360">Esto es útil cuando se consultan datos semiestructurados o de tipos combinados.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="fb4bf-361">Por ejemplo, esta consulta devuelve Hola "Apellidos" Si está presente, o hello "apellido" Si no están presente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="fb4bf-362"><a id="EscapingReservedKeywords"></a>Descriptor de acceso de propiedad entre comillas</span><span class="sxs-lookup"><span data-stu-id="fb4bf-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="fb4bf-363">También puede tener acceso a propiedades mediante el operador de la propiedad indicada de hello `[]`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="fb4bf-364">Por ejemplo, `SELECT c.grade` and `SELECT c["grade"]` son equivalentes.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="fb4bf-365">Esta sintaxis es útil cuando necesita tooescape una propiedad que contiene espacios, caracteres especiales, u ocurre hello tooshare mismo nombre como una palabra clave SQL o una palabra reservada.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="fb4bf-366"><a id="SelectClause"></a>Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="fb4bf-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="fb4bf-367">cláusula SELECT Hello (**`SELECT <select_list>`**) es obligatorio y especifica qué valores se recuperan de la consulta de hello, igual que en ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="fb4bf-368">subconjunto de Hola que se han filtrado encima de los documentos de origen de Hola se pasan en la fase de proyección de hello, donde hello especificada se recuperan valores JSON y se construye un nuevo objeto JSON, para cada entrada que se pasó en él.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="fb4bf-369">Hola de ejemplo siguiente muestra una consulta SELECT normal.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="fb4bf-370">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-371">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="fb4bf-372">Propiedades anidadas</span><span class="sxs-lookup"><span data-stu-id="fb4bf-372">Nested properties</span></span>
<span data-ttu-id="fb4bf-373">En el siguiente ejemplo de Hola, nos estamos proyectar dos propiedades anidadas `f.address.state` y `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="fb4bf-374">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-375">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="fb4bf-376">Proyección también admite expresiones de JSON como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="fb4bf-377">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-378">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="fb4bf-379">Echemos un vistazo a la función hello de `$1` aquí.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="fb4bf-380">Hola `SELECT` cláusula necesita toocreate un objeto JSON y puesto que se proporcionó ninguna clave, usamos los nombres de variable argumento implícito a partir de `$1`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="fb4bf-381">Por ejemplo, esta consulta devuelve dos variables de argumentos implícitos, etiquetadas como `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="fb4bf-382">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-383">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="fb4bf-384">Establecimiento de alias</span><span class="sxs-lookup"><span data-stu-id="fb4bf-384">Aliasing</span></span>
<span data-ttu-id="fb4bf-385">Ahora vamos a ampliar el ejemplo de Hola anteriormente con alias explícito de valores.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="fb4bf-386">TAL cual Hola palabra clave utilizada para el alias.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="fb4bf-387">Es opcional, como se muestra mientras que el valor de segundo Hola proyectar como `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="fb4bf-388">En caso de que una consulta tiene dos propiedades con hello mismo nombre, alias deben ser toorename usa uno o ambos de Hola propiedades para que se elimina la ambigüedad en hello proyectada resultados.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="fb4bf-389">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-390">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="fb4bf-391">Expresiones escalares</span><span class="sxs-lookup"><span data-stu-id="fb4bf-391">Scalar expressions</span></span>
<span data-ttu-id="fb4bf-392">También hace referencia a tooproperty, también admite la cláusula SELECT Hola expresiones escalares como constantes, expresiones aritméticas, expresiones lógicas, etcetera. Por ejemplo, aquí hay una sencilla consulta "Hello World".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="fb4bf-393">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="fb4bf-394">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="fb4bf-395">A continuación se muestra un ejemplo más complejo que usa una expresión escalar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="fb4bf-396">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="fb4bf-397">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="fb4bf-398">En el siguiente ejemplo de Hola, resultado de hello de expresión escalar de hello es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="fb4bf-399">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="fb4bf-400">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="fb4bf-401">Creación de objetos y matrices</span><span class="sxs-lookup"><span data-stu-id="fb4bf-401">Object and array creation</span></span>
<span data-ttu-id="fb4bf-402">Otra característica clave del lenguaje SQL de la API de DocumentDB es la creación de matrices u objetos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="fb4bf-403">En el ejemplo anterior de hello, tenga en cuenta que hemos creado un nuevo objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="fb4bf-404">De forma similar, uno puede construir matrices de tal y como se muestra en hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="fb4bf-405">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="fb4bf-406">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-406">**Results**</span></span>  

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

### <span data-ttu-id="fb4bf-407"><a id="ValueKeyword"></a>Palabra clave VALUE</span><span class="sxs-lookup"><span data-stu-id="fb4bf-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="fb4bf-408">Hola **valor** (palabra clave) proporciona un valor de manera tooreturn JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="fb4bf-409">Por ejemplo, las consultas de Hola se muestra a continuación devuelve Hola escalar `"Hello World"` en lugar de `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="fb4bf-410">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="fb4bf-411">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="fb4bf-412">Hello consulta siguiente devuelve valor JSON de hello sin hello `"address"` etiqueta en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="fb4bf-413">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="fb4bf-414">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-414">**Results**</span></span>  

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

<span data-ttu-id="fb4bf-415">Hello en el ejemplo siguiente se amplía este tooshow cómo tooreturn valores primitivos de JSON (nivel de hello hoja del árbol JSON de hello).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="fb4bf-416">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="fb4bf-417">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="fb4bf-418">Operador *</span><span class="sxs-lookup"><span data-stu-id="fb4bf-418">* Operator</span></span>
<span data-ttu-id="fb4bf-419">operador especial (*) Hello es documento de hello tooproject compatibles como-es.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="fb4bf-420">Cuando se utiliza, debe ser Hola proyecta solo campo.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="fb4bf-421">Aunque una consulta como `SELECT * FROM Families f` es válida, `SELECT VALUE * FROM Families f ` y `SELECT *, f.id FROM Families f ` no lo son.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="fb4bf-422">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fb4bf-423">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-423">**Results**</span></span>

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

### <span data-ttu-id="fb4bf-424"><a id="TopKeyword"></a>Operador TOP</span><span class="sxs-lookup"><span data-stu-id="fb4bf-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="fb4bf-425">puede ser la palabra clave TOP de Hello usar toolimit Hola un número de valores de una consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="fb4bf-426">Cuando se usa TOP junto con la cláusula ORDER BY hello, conjunto de resultados de hello es toohello limitado el primer número N de valores ordenados; en caso contrario, devuelve Hola primer N número de resultados en un orden indefinido.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="fb4bf-427">Como práctica recomendada, en una instrucción SELECT, utilice siempre una cláusula ORDER BY con la cláusula TOP Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="fb4bf-428">Se trata de una única manera de hello toopredictably indicar qué filas están afectadas por la parte superior.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="fb4bf-429">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="fb4bf-430">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-430">**Results**</span></span>

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

<span data-ttu-id="fb4bf-431">TOP se puede usar con un valor constante (como se muestra anteriormente) o con un valor variable usando consultas con parámetros.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="fb4bf-432">Si desea obtener más información, consulte las consultas con parámetros que aparecen a continuación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="fb4bf-433"><a id="Aggregates"></a>Funciones de agregado</span><span class="sxs-lookup"><span data-stu-id="fb4bf-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="fb4bf-434">También puede realizar agregaciones en hello `SELECT` cláusula.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="fb4bf-435">Las funciones de agregado realizan un cálculo en un conjunto de valores y devuelven un valor único.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="fb4bf-436">Por ejemplo, hello siguiente consulta devuelve Hola recuento de familias documentos dentro de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="fb4bf-437">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="fb4bf-438">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="fb4bf-439">También puede devolver valor escalar de Hola de hello agregado mediante el uso de hello `VALUE` palabra clave.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="fb4bf-440">Por ejemplo, hello siguiente consulta devuelve Hola recuento de valores como un único número:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="fb4bf-441">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="fb4bf-442">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="fb4bf-443">También puede realizar agregados en combinación con filtros.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="fb4bf-444">Por ejemplo, hello siguiente consulta devuelve Hola recuento de documentos con la dirección de hello en hello estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="fb4bf-445">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="fb4bf-446">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="fb4bf-447">Hello siguiente tabla muestra hello lista de funciones de agregado compatibles en la API de documentos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="fb4bf-448">`SUM`y `AVG` se aplican a valores numéricos, mientras que `COUNT`, `MIN` y `MAX` se pueden aplicar a números, cadenas, y valores booleanos y NULL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="fb4bf-449">Uso</span><span class="sxs-lookup"><span data-stu-id="fb4bf-449">Usage</span></span> | <span data-ttu-id="fb4bf-450">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb4bf-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="fb4bf-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="fb4bf-451">COUNT</span></span> | <span data-ttu-id="fb4bf-452">Devuelve Hola número de elementos de la expresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="fb4bf-453">SUM</span><span class="sxs-lookup"><span data-stu-id="fb4bf-453">SUM</span></span>   | <span data-ttu-id="fb4bf-454">Devuelve Hola suma de todos los valores de hello en la expresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="fb4bf-455">MÍN</span><span class="sxs-lookup"><span data-stu-id="fb4bf-455">MIN</span></span>   | <span data-ttu-id="fb4bf-456">Devuelve Hola valor mínimo en expresión Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="fb4bf-457">MÁX</span><span class="sxs-lookup"><span data-stu-id="fb4bf-457">MAX</span></span>   | <span data-ttu-id="fb4bf-458">Devuelve Hola valor máximo en expresión Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="fb4bf-459">MEDIA</span><span class="sxs-lookup"><span data-stu-id="fb4bf-459">AVG</span></span>   | <span data-ttu-id="fb4bf-460">Devuelve Hola promedio de valores de hello en la expresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="fb4bf-461">También se pueden realizar agregados sobre resultados de Hola de una iteración de la matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="fb4bf-462">Para más información, vea [Iteración de matriz en consultas](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="fb4bf-463">Al usar hello Explorador de consulta del portal de Azure, tenga en cuenta que las consultas de agregación pueden devolver Hola resultados parcialmente agregados a través de una página de consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="fb4bf-464">Hola SDK genera un único valor acumulado en todas las páginas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="fb4bf-465">Orden en consultas de agregación de tooperform mediante código, se necesita .NET SDK 1.12.0, .NET Core SDK 1.1.0 o Java SDK 1.9.5 o superior.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="fb4bf-466"><a id="OrderByClause"></a>Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="fb4bf-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="fb4bf-467">Al igual que en ANSI SQL, puede incluir una cláusula Order By opcional al realizar la consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="fb4bf-468">cláusula de Hello puede incluir en el que se deben recuperar los resultados de un pedido de Hola de toospecify de argumento ASC o DESC opcional.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="fb4bf-469">Por ejemplo, aquí es una consulta que recupera familias en orden de nombre de ciudad residente Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="fb4bf-470">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="fb4bf-471">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-471">**Results**</span></span>

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

<span data-ttu-id="fb4bf-472">Y aquí es una consulta que recupera familias en orden de fecha de creación, que se almacena como un número que representa Hola tiempo base, es decir, tiempo transcurrido desde el 1 de enero de 1970 en segundos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="fb4bf-473">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="fb4bf-474">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-474">**Results**</span></span>

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

## <span data-ttu-id="fb4bf-475"><a id="Advanced"></a>Conceptos avanzados de base de datos y consultas SQL</span><span class="sxs-lookup"><span data-stu-id="fb4bf-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="fb4bf-476"><a id="Iteration"></a>Iteración</span><span class="sxs-lookup"><span data-stu-id="fb4bf-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="fb4bf-477">Se agregó una nueva construcción a través de hello **IN** palabra clave en la compatibilidad de documentos API SQL tooprovide para iterar por matrices JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="fb4bf-478">origen de Hello FROM proporciona compatibilidad para la iteración.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="fb4bf-479">Puede empezar con el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-479">Let's start with hello following example:</span></span>

<span data-ttu-id="fb4bf-480">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="fb4bf-481">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-481">**Results**</span></span>  

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

<span data-ttu-id="fb4bf-482">Ahora Echemos un vistazo a otra consulta que realiza iteración en los elementos secundarios en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="fb4bf-483">Tenga en cuenta diferencia hello en la matriz de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="fb4bf-484">Este ejemplo divide `children` y reduce los resultados de hello en una sola matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="fb4bf-485">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="fb4bf-486">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-486">**Results**</span></span>  

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

<span data-ttu-id="fb4bf-487">Esto puede resultar más toofilter usado en cada entrada de matriz de hello tal y como se muestra en el siguiente ejemplo de Hola individual:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="fb4bf-488">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="fb4bf-489">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="fb4bf-490">También puede realizar la agregación sobre resultado de hello de iteración de la matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="fb4bf-491">Por ejemplo, hello consulta siguiente cuenta Hola número de elementos secundarios entre todas las familias.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="fb4bf-492">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="fb4bf-493">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="fb4bf-494"><a id="Joins"></a>Combinaciones</span><span class="sxs-lookup"><span data-stu-id="fb4bf-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="fb4bf-495">En una base de datos relacional, es importante Hola necesidad toojoin entre tablas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="fb4bf-496">Su Hola lógico toodesigning corollary normalizado esquemas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="fb4bf-497">Modelo de datos sin normalizar Hola de documentos de esquema se ocupa contrarias toothis, API de documentos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="fb4bf-498">Esto es equivalente lógico de Hola de un "autocombinación".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="fb4bf-499">sintaxis de Hola que admite el lenguaje de hello es la combinación de combinación < from_source2 > < from_source1 >... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="fb4bf-500">Generalmente, esto devuelve un conjunto de **N** tuplas (tupla con **N** valores).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="fb4bf-501">Cada tupla tiene valores generados por sus respectivos conjuntos en iteración de todos los alias de colección.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="fb4bf-502">En otras palabras, se trata de un producto cruzado completo de conjuntos de hello participan en la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="fb4bf-503">Hello en los ejemplos siguientes muestran cómo funciona la cláusula de combinación Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="fb4bf-504">En el siguiente ejemplo de Hola, resultado de hello está vacía ya que hello producto cruzado de todos los documentos de origen y un conjunto vacío está vacío.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="fb4bf-505">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="fb4bf-506">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="fb4bf-507">En el siguiente ejemplo de Hola, combinación de hello es entre hello y raíz del documento hello `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="fb4bf-508">Es un producto cruzado entre dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="fb4bf-509">ausencia de Hola que los elementos secundarios es una matriz no es eficaz en hello combinación puesto que estamos trabajando con una única raíz que es la matriz de elementos secundarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="fb4bf-510">Por lo tanto, el resultado de hello contiene solo dos resultados, ya que el producto cruzado de todos los documentos con la matriz de Hola Hola produce exactamente un único documento.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="fb4bf-511">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="fb4bf-512">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="fb4bf-513">Hola de ejemplo siguiente muestra una combinación más convencional:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="fb4bf-514">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="fb4bf-515">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-515">**Results**</span></span>

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



<span data-ttu-id="fb4bf-516">Hello lo primero que toonote es ese hello `from_source` de hello **UNIR** cláusula es un iterador.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="fb4bf-517">Por lo tanto, el flujo de hello en este caso es como sigue:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="fb4bf-518">Expanda cada elemento secundario **c** de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="fb4bf-519">Aplicar un producto cruzado con raíz Hola de documento de hello **f** con cada elemento secundario **c** que se acoplan en el primer paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="fb4bf-520">Por último, el objeto de raíz de Hola de proyecto **f** name (propiedad) independiente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="fb4bf-521">primer documento de Hello (`AndersenFamily`) contiene un único elemento secundario, por lo que el conjunto de resultados de hello contiene sólo un único objeto toothis documento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="fb4bf-522">segundo documento de Hello (`WakefieldFamily`) contiene dos elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="fb4bf-523">Por lo tanto, hello producto cruzado genera un objeto independiente para cada elemento secundario, lo que resulta en dos objetos, uno para cada documento de toothis secundarios correspondientes.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="fb4bf-524">raíz de Hello campos en ambos estos documentos son iguales, Hola como se esperaría en un producto cruzado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="fb4bf-525">Hola utilidad real de hello combinación es tooform tuplas desde el producto cruzado de hello en una forma que en caso contrario es difícil tooproject.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="fb4bf-526">Además, tal y como se ve en el siguiente ejemplo de Hola, puede filtrar en la combinación de Hola de una tupla Hola que permite el usuario eligió una condición satisface Hola tuplas general.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="fb4bf-527">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="fb4bf-528">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-528">**Results**</span></span>

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



<span data-ttu-id="fb4bf-529">Este ejemplo es una extensión natural del anterior ejemplo de Hola y realiza una combinación de tipo double.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="fb4bf-530">Por lo tanto, hello producto cruzado puede verse como Hola siguiente pseudocódigo:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

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

<span data-ttu-id="fb4bf-531">`AndersenFamily` tiene un hijo que tiene una mascota.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="fb4bf-532">Por lo tanto, hello producto cruzado da como resultado una fila (1\*1\*1) de esta familia.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="fb4bf-533">La familia Wakefield tiene, sin embargo, dos hijos, pero solo uno, "Jesse", tiene mascotas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="fb4bf-534">Pero Jesse tiene dos mascotas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-534">Jesse has two pets though.</span></span> <span data-ttu-id="fb4bf-535">Por lo tanto, hello producto cruzado genera 1\*1\*2 = 2 filas de esta familia.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="fb4bf-536">En el siguiente ejemplo de Hola, hay un filtro adicional en `pet`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="fb4bf-537">Esto excluye todas las tuplas de Hola donde hello mascota nombre no es "Instantáneas".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="fb4bf-538">Tenga en cuenta que estamos toobuild capaz de tuplas de matrices, filtrar por cualquiera de los elementos de Hola de tupla de hello y cualquier combinación de elementos de hello del proyecto.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="fb4bf-539">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="fb4bf-540">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="fb4bf-541"><a id="JavaScriptIntegration"></a>Integración de JavaScript</span><span class="sxs-lookup"><span data-stu-id="fb4bf-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="fb4bf-542">Base de datos de Azure Cosmos proporciona un modelo de programación para ejecutar lógica de la aplicación de JavaScript que se basa directamente en las colecciones de hello en cuanto a los procedimientos almacenados y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="fb4bf-543">Esto les proporciona:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-543">This allows for both:</span></span>

* <span data-ttu-id="fb4bf-544">Operaciones de CRUD transaccionales de alto rendimiento de toodo de capacidad y consultas en documentos de una colección en virtud de la integración de JavaScript en tiempo de ejecución directamente en el motor de base de datos de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="fb4bf-545">Un modelo natural de flujo de control, ámbito variable, asignación e integración de primitivas de control de excepciones con transacciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="fb4bf-546">Para obtener más detalles sobre la compatibilidad de base de datos de Azure Cosmos para la integración de JavaScript, por favor, consulte la documentación de programación del servidor de JavaScript de toohello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="fb4bf-547"><a id="UserDefinedFunctions"></a>Funciones definidas por el usuario (UDF)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="fb4bf-548">Junto con los tipos de hello ya definidos en este artículo, DocumentDB API SQL proporciona compatibilidad para las funciones definida por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="fb4bf-549">En concreto, se admiten UDF escalares donde los desarrolladores de hello pueden pasar en cero o varios argumentos y devuelven un resultado único argumento.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="fb4bf-550">Cada uno de estos argumentos se comprueba para ver si se trata de valores JSON válidos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="fb4bf-551">Hola sintaxis SQL de la API de documentos se extiende la lógica de la aplicación personalizada de toosupport uso de estas funciones definidas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="fb4bf-552">Las funciones definidas por el usuario pueden registrarse con la API de DocumentDB y, a continuación, se puede hacer referencia a ellas como parte de una consulta de SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="fb4bf-553">De hecho, Hola UDF son exquisitely diseñado toobe invocado por las consultas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="fb4bf-554">Como una opción toothis corollary, UDF no tiene el objeto de contexto de acceso toohello que Hola otras JavaScript tienen tipos (procedimientos almacenados y desencadenadores).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="fb4bf-555">Puesto que las consultas se ejecutan como de solo lectura, pueden ejecutarse en réplicas principales o secundarias.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="fb4bf-556">Por lo tanto, las UDF son toorun diseñado en las réplicas secundarias a diferencia de otros tipos de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="fb4bf-557">A continuación se muestra un ejemplo de cómo se puede registrar una UDF en Hola DB Cosmos base de datos, en concreto en una colección de documentos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="fb4bf-558">Hello en el ejemplo anterior se crea una UDF cuyo nombre es `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="fb4bf-559">Acepta dos valores de cadena JSON `input` y `pattern` y comprueba si la primeras coincidencias de hello especifica el patrón de hello en segundo lugar Hola con función de JavaScript a String.Match.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="fb4bf-560">Ahora podemos usar esta UDF en una consulta de una proyección.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="fb4bf-561">UDF se deben calificar con el prefijo entre mayúsculas y minúsculas de Hola "udf."</span><span class="sxs-lookup"><span data-stu-id="fb4bf-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="fb4bf-562">cuando se las llama desde las consultas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="fb4bf-563">Anterior too3/17/2015, Cosmos DB admite llamadas a UDF sin Hola "udf."</span><span class="sxs-lookup"><span data-stu-id="fb4bf-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="fb4bf-564">al igual que SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="fb4bf-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="fb4bf-565">Este patrón de llamada está desusado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="fb4bf-566">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="fb4bf-567">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="fb4bf-568">Hola UDF también puede utilizarse dentro de un filtro como se muestra en el ejemplo de Hola siguiente, también está calificado con hello "udf."</span><span class="sxs-lookup"><span data-stu-id="fb4bf-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="fb4bf-569">prefijo:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-569">prefix:</span></span>

<span data-ttu-id="fb4bf-570">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="fb4bf-571">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="fb4bf-572">Básicamente, las UDF son expresiones escalares válidas y pueden usarse en ambas proyecciones y filtros.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="fb4bf-573">tooexpand en potencia Hola de UDF, echemos un vistazo a otro ejemplo con una lógica condicional:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="fb4bf-574">A continuación se muestra un ejemplo que ejercicios Hola UDF.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="fb4bf-575">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="fb4bf-576">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-576">**Results**</span></span>

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


<span data-ttu-id="fb4bf-577">Como hello showcase de ejemplos anteriores, las UDF integran potencia de Hola de lenguaje JavaScript con hello documentos API SQL tooprovide una interfaz programable enriquecida toodo procedimientos, condicional una lógica compleja con ayuda de Hola de integradas en tiempo de ejecución de JavaScript capacidades.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="fb4bf-578">Documentos API SQL proporciona argumentos de hello toohello UDF para cada documento de origen de Hola Hola actual fase (cláusula WHERE o cláusula SELECT) de procesamiento Hola UDF.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="fb4bf-579">Hello resultado se incorpora Hola general canalización de ejecución sin problemas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="fb4bf-580">Si propiedades hello tooby que se hace referencia Hola UDF parámetros no están disponibles en el valor JSON, Hola hello parámetro se considera como sin definir y, por tanto, Hola invocación UDF completamente se omite.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="fb4bf-581">De forma similar si el resultado de hello de hello UDF no está definido, no se incluye en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="fb4bf-582">En resumen, las UDF son lógica de negocios compleja de buenas herramientas toodo como parte de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="fb4bf-583">Evaluación de operadores</span><span class="sxs-lookup"><span data-stu-id="fb4bf-583">Operator evaluation</span></span>
<span data-ttu-id="fb4bf-584">COSMOS DB, en virtud de Hola de ser una base de datos JSON dibuja parallels con operadores de JavaScript y su semántica de evaluación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="fb4bf-585">Mientras la base de datos de Cosmos intenta toopreserve semántica de JavaScript en términos de soporte JSON, se desvía la evaluación de la operación de hello en algunos casos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="fb4bf-586">En SQL de la API de documentos, a diferencia de en SQL tradicional, tipos de Hola de valores a menudo no se conocen hasta que se recuperan valores de hello de base de datos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="fb4bf-587">En orden tooefficiently ejecutar consultas, la mayoría de los operadores de Hola tienen estrictos requisitos de tipos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="fb4bf-588">SQL de la API de DocumentDB no realiza conversiones implícitas a diferencia de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="fb4bf-589">Por ejemplo, una consulta como `SELECT * FROM Person p WHERE p.Age = 21` coincide con documentos que contienen una propiedad Age cuyo valor es 21.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="fb4bf-590">Cualquier otro documento cuya propiedad Age coincida con la cadena "21", u otras variaciones posiblemente infinitas, como "021", "21,0", "0021", "00021", etc. no producirán coincidencias.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="fb4bf-591">Se trata en cambio toohello JavaScript donde los valores de cadena de hello son toonumbers realiza una conversión implícita (en función de operador, por ejemplo: ==).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="fb4bf-592">Esta opción es fundamental para conseguir una coincidencia de índices eficaz en SQL de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="fb4bf-593">Consultas SQL con parámetros</span><span class="sxs-lookup"><span data-stu-id="fb4bf-593">Parameterized SQL queries</span></span>
<span data-ttu-id="fb4bf-594">COSMOS DB admite consultas con parámetros expresados con hello familiarizado notación @.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="fb4bf-595">El uso de SQL con parámetros permite controlar y evitar de forma sólida la entrada por parte de los usuarios, impidiendo así la exposición accidental de datos a través de la inyección de código SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="fb4bf-596">Por ejemplo, puede escribir una consulta que acepte los apellidos y el estado de la dirección como parámetros y, a continuación, ejecutarla para distintos valores de los parámetros mencionados en función de la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="fb4bf-597">Esta solicitud, a continuación, se puede enviar tooCosmos base de datos como una consulta con parámetros de JSON como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="fb4bf-598">Hola argumento tooTOP puede establecerse utilizando consultas con parámetros como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="fb4bf-599">Los valores de los parámetros pueden ser cualquier tipo de JSON válido (cadenas, números, booleanos, null o incluso matrices o JSON anidado).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="fb4bf-600">Además, como Cosmos DB no tiene ningún esquema, los parámetros no se validan respecto a ningún tipo.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="fb4bf-601"><a id="BuiltinFunctions"></a>Funciones integradas</span><span class="sxs-lookup"><span data-stu-id="fb4bf-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="fb4bf-602">Cosmos DB también admite un número de funciones integradas para operaciones comunes, que se pueden usar dentro de las consultas como funciones definidas por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="fb4bf-603">Grupo de funciones</span><span class="sxs-lookup"><span data-stu-id="fb4bf-603">Function group</span></span>          | <span data-ttu-id="fb4bf-604">Operaciones</span><span class="sxs-lookup"><span data-stu-id="fb4bf-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fb4bf-605">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="fb4bf-605">Mathematical functions</span></span>  | <span data-ttu-id="fb4bf-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN y TAN</span><span class="sxs-lookup"><span data-stu-id="fb4bf-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="fb4bf-607">Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-607">Type checking functions</span></span> | <span data-ttu-id="fb4bf-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="fb4bf-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="fb4bf-609">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="fb4bf-609">String functions</span></span>        | <span data-ttu-id="fb4bf-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING y UPPER</span><span class="sxs-lookup"><span data-stu-id="fb4bf-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="fb4bf-611">Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="fb4bf-611">Array functions</span></span>         | <span data-ttu-id="fb4bf-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH y ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="fb4bf-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="fb4bf-613">Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="fb4bf-613">Spatial functions</span></span>       | <span data-ttu-id="fb4bf-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID y ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="fb4bf-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="fb4bf-615">Si actualmente usa una función definida por el usuario (UDF) para el que ahora está disponible una función integrada, debe usar la función integrada correspondiente de hello tal y como se va toorun más rápida de toobe y mucho más eficaz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="fb4bf-616">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="fb4bf-616">Mathematical functions</span></span>
<span data-ttu-id="fb4bf-617">Hola funciones matemáticas cada realizan un cálculo, en función de los valores de entrada que se proporcionan como argumentos y devuelven un valor numérico.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="fb4bf-618">Esta es una tabla de las funciones matemáticas integradas admitidas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="fb4bf-619">Uso</span><span class="sxs-lookup"><span data-stu-id="fb4bf-619">Usage</span></span> | <span data-ttu-id="fb4bf-620">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb4bf-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fb4bf-621">[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="fb4bf-622">Devuelve Hola valor absoluto (positivo) de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="fb4bf-624">Devuelve Hola valor entero más pequeño mayor o igual a, Hola expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="fb4bf-626">Devuelve Hola mayor entero menor o igual toohello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="fb4bf-628">Exponente de hello devuelve de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="fb4bf-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="fb4bf-630">Devuelve el logaritmo de natural de Hola de hello especificados expresión numérica, o logaritmo hello mediante Hola especificados base</span><span class="sxs-lookup"><span data-stu-id="fb4bf-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="fb4bf-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="fb4bf-632">Hola devuelve base 10 valores logarítmico de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="fb4bf-634">Devuelve un valor numérico, redondeado toohello valor de entero más cercano.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="fb4bf-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="fb4bf-636">Devuelve un valor numérico, el valor entero más cercano de toohello truncado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="fb4bf-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="fb4bf-638">Devuelve Hola cuadrado raíz de hello especificado expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="fb4bf-640">Hola devuelve cuadrado de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="fb4bf-642">Devuelve Hola power de hello especificado expresión numérica toohello valor especificado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="fb4bf-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="fb4bf-644">Expresión numérica especifica devuelve Hola inicio de sesión valor (-1, 0, 1) de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="fb4bf-646">Ángulo de hello devuelve, en radianes, cuyo coseno es Hola expresión numérica especificada; También se denomina arco coseno.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="fb4bf-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="fb4bf-648">Ángulo de hello devuelve, en radianes, cuyo seno es hello especifica expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="fb4bf-649">También se denomina arcoseno.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="fb4bf-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="fb4bf-651">Ángulo de hello devuelve, en radianes, cuya tangente es hello especifica expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="fb4bf-652">También se denomina arcotangente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="fb4bf-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="fb4bf-654">Devuelve Hola ángulo, en radianes, entre el eje x positivo de Hola y rayo de Hola desde el punto de hello origen toohello (y, x), donde x e y son valores de hello de hello dos expresiones de tipo flotante especificado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="fb4bf-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="fb4bf-656">Devuelve Hola coseno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="fb4bf-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="fb4bf-658">Devuelve Hola cotangente trigonométrica Hola especifica el ángulo, en radianes, en hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="fb4bf-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="fb4bf-660">Devuelve Hola ángulo correspondiente en grados para un ángulo especificado en radianes.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="fb4bf-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="fb4bf-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="fb4bf-662">Devuelve Hola valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="fb4bf-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="fb4bf-664">Devuelve radianes cuando se especifica una expresión numérica en grados.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="fb4bf-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="fb4bf-666">Devuelve Hola seno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="fb4bf-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="fb4bf-668">Tangente de hello devuelve de expresión de entrada de hello, Hola la expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="fb4bf-669">Por ejemplo, ahora puede ejecutar las consultas como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="fb4bf-670">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="fb4bf-671">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-671">**Results**</span></span>

    [4]

<span data-ttu-id="fb4bf-672">Hola principal diferencia entre tooANSI de funciones en comparación de Cosmos DB SQL es que son toowork diseñado correctamente con los datos del esquema sin esquema y mixto.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="fb4bf-673">Por ejemplo, si tiene un documento donde falta la propiedad de tamaño de Hola o tiene un valor no numérico, como "desconocido", a continuación, documento hello es recién saltado por, en lugar de devolver un error.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="fb4bf-674">Funciones de comprobación de tipos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-674">Type checking functions</span></span>
<span data-ttu-id="fb4bf-675">funciones de comprobación de tipo Hello permiten a tipo de hello toocheck de una expresión dentro de las consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="fb4bf-676">Funciones de comprobación pueden ser de tipo usa el tipo de hello toodetermine de propiedades de los documentos en marcha de hello cuando se variable o desconocido.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="fb4bf-677">Esta es una tabla de las funciones de comprobación de tipos integradas admitidas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="fb4bf-678"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="fb4bf-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="fb4bf-679"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="fb4bf-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-681">Devuelve un valor booleano que indica si el tipo de hello del valor de hello es una matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-683">Devuelve un valor booleano que indica si el tipo de hello del valor de hello es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-685">Devuelve un valor booleano que indica si el tipo de saludo del valor de hello es null.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-687">Devuelve un valor booleano que indica si el tipo de hello del valor de hello es un número.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-689">Devuelve un valor booleano que indica si el tipo de hello del valor de hello es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-691">Devuelve un valor booleano que indica si el tipo de saludo del valor de hello es una cadena.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-693">Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="fb4bf-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="fb4bf-695">Devuelve un valor booleano que indica si el tipo de saludo del valor de hello es una cadena, número, booleano o null.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="fb4bf-696">Uso de estas funciones, ahora puede ejecutar las consultas como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="fb4bf-697">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="fb4bf-698">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="fb4bf-699">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="fb4bf-699">String functions</span></span>
<span data-ttu-id="fb4bf-700">Hola siguientes funciones escalares realizan una operación sobre un valor de cadena de entrada y devuelven una cadena, valor numérico o booleano.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="fb4bf-701">A continuación se facilita una tabla de funciones de cadena integradas:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="fb4bf-702">Uso</span><span class="sxs-lookup"><span data-stu-id="fb4bf-702">Usage</span></span> | <span data-ttu-id="fb4bf-703">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb4bf-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fb4bf-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="fb4bf-705">Devuelve el número de caracteres de Hola Hola especifica la expresión de cadena</span><span class="sxs-lookup"><span data-stu-id="fb4bf-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="fb4bf-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="fb4bf-707">Devuelve una cadena que es el resultado de hello de concatenar dos o más valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="fb4bf-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="fb4bf-709">Devuelve parte de una expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="fb4bf-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="fb4bf-711">Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar</span><span class="sxs-lookup"><span data-stu-id="fb4bf-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="fb4bf-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="fb4bf-713">Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar</span><span class="sxs-lookup"><span data-stu-id="fb4bf-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="fb4bf-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="fb4bf-715">Devuelve un valor booleano que indica si primera expresión de cadena hello contiene hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="fb4bf-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="fb4bf-717">Devuelve Hola a partir de la posición de la primera aparición de hello de la segunda expresión de cadena Hola dentro de la primera expresión de cadena especificada de hello, o -1 si no se encuentra la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="fb4bf-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="fb4bf-719">Devuelve Hola parte izquierda de una cadena con hello especificada número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="fb4bf-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="fb4bf-721">Hola devuelve parte derecha de una cadena con hello del número de caracteres especificado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="fb4bf-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="fb4bf-723">Devuelve una expresión de cadena después de quitar los espacios en blanco iniciales.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="fb4bf-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="fb4bf-725">Devuelve una expresión de cadena después de truncar todos los espacios en blanco finales.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="fb4bf-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="fb4bf-727">Devuelve una expresión de cadena después de convertir toolowercase de datos de caracteres en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="fb4bf-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="fb4bf-729">Devuelve una expresión de cadena después de convertir toouppercase de datos de carácter en minúscula.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="fb4bf-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="fb4bf-731">Reemplaza todas las apariciones de un valor de cadena especificado por otro valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="fb4bf-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="fb4bf-733">Repite un valor de cadena un número especificado de veces.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="fb4bf-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="fb4bf-735">Devuelve Hola invirtiendo el orden de un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="fb4bf-736">Uso de estas funciones, ahora puede ejecutar las consultas como Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="fb4bf-737">Por ejemplo, puede devolver el nombre de familia de Hola en mayúsculas como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="fb4bf-738">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="fb4bf-739">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="fb4bf-740">O concatenar cadenas como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="fb4bf-741">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="fb4bf-742">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="fb4bf-743">Funciones de cadena también pueden utilizarse en Hola donde cláusula toofilter obtener los resultados, al igual que en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="fb4bf-744">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="fb4bf-745">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="fb4bf-746">Funciones de matriz</span><span class="sxs-lookup"><span data-stu-id="fb4bf-746">Array functions</span></span>
<span data-ttu-id="fb4bf-747">Hola siguientes funciones escalares realiza una operación sobre un valor de entrada de matriz y devolución numérico, el valor booleano o de matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="fb4bf-748">A continuación se facilita una tabla de funciones de matriz integradas:</span><span class="sxs-lookup"><span data-stu-id="fb4bf-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="fb4bf-749">Uso</span><span class="sxs-lookup"><span data-stu-id="fb4bf-749">Usage</span></span> | <span data-ttu-id="fb4bf-750">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb4bf-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fb4bf-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="fb4bf-752">Devuelve el número de elementos de Hola Hola especifica la expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="fb4bf-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="fb4bf-754">Devuelve una matriz que es el resultado de hello de concatenar dos o más valores de la matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="fb4bf-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="fb4bf-756">Devuelve un valor booleano que indica si la matriz de hello contiene Hola valor especificado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="fb4bf-757">Puede especificar si la coincidencia de hello es completa o parcial.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="fb4bf-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="fb4bf-759">Devuelve parte de una expresión de matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="fb4bf-760">Funciones de matriz pueden ser matrices de toomanipulate usado en JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="fb4bf-761">Por ejemplo, aquí es una consulta que devuelve todos los documentos donde uno de los elementos primarios de hello es "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="fb4bf-762">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="fb4bf-763">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="fb4bf-764">Puede especificar un fragmento parcial de elementos coincidentes en la matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="fb4bf-765">Hello siguiente consulta busca todos los elementos primarios con hello `givenName` de `Robin`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="fb4bf-766">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="fb4bf-767">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="fb4bf-768">Este es otro ejemplo que utiliza ARRAY_LENGTH tooget Hola número de hijos por familia.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="fb4bf-769">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="fb4bf-770">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="fb4bf-771">Funciones espaciales</span><span class="sxs-lookup"><span data-stu-id="fb4bf-771">Spatial functions</span></span>
<span data-ttu-id="fb4bf-772">COSMOS DB admite Hola siguiendo las funciones integradas de Open Geospatial Consortium (OGC) para realizar consultas geoespaciales.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="fb4bf-773"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="fb4bf-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="fb4bf-774"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="fb4bf-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="fb4bf-776">Devuelve la distancia de hello entre expresiones de punto de GeoJSON, polígono o LineString Hola dos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="fb4bf-778">Devuelve una expresión booleana que indica si es Hola primer GeoJSON objeto (punto, polígono o LineString) dentro de hello segundo GeoJSON objeto (punto, polígono o LineString).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="fb4bf-780">Devuelve una expresión booleana que indica si se intersecan Hola dos GeoJSON objetos especificados (punto, polígono o LineString).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="fb4bf-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="fb4bf-782">Devuelve un valor booleano que indica si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fb4bf-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="fb4bf-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="fb4bf-784">Devuelve un valor JSON que contiene un valor booleano si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida y si no es válido, además Hola motivo como un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="fb4bf-785">Funciones espaciales pueden ser consultas de proximidad de tooperform utilizadas en los datos espaciales.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="fb4bf-786">Por ejemplo, aquí es una consulta que devuelve la que familia de todos los documentos que está dentro de 30 km de hello ubicación especificada mediante hello ST_DISTANCE función integrada.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="fb4bf-787">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="fb4bf-788">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="fb4bf-789">Para más información sobre la compatibilidad geoespacial en Cosmos DB, consulte [Uso de datos geoespaciales en Azure Cosmos DB](geospatial.md),</span><span class="sxs-lookup"><span data-stu-id="fb4bf-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="fb4bf-790">Que concluye funciones espaciales y Hola sintaxis SQL para la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="fb4bf-791">Ahora Echemos un vistazo a cómo LINQ consultar funciona y cómo interactúa con la sintaxis de Hola que hemos visto hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="fb4bf-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="fb4bf-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="fb4bf-793">LINQ es un modelo de programación de .NET que expresa cálculos como consultas de secuencias de objetos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="fb4bf-794">COSMOS DB proporciona un toointerface de biblioteca de cliente con LINQ al facilitar una conversión entre los objetos JSON y .NET y una asignación entre un subconjunto de LINQ consulta tooCosmos DB consultas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="fb4bf-795">Figura Hola siguiente muestra la arquitectura de Hola de admitir consultas LINQ usando la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="fb4bf-796">Con cliente de base de datos de Cosmos hello, los programadores pueden crear un **IQueryable** que directamente consultas Hola DB Cosmos consultar al proveedor, que luego convierte la consulta LINQ de hello en una consulta de base de datos de Cosmos del objeto.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="fb4bf-797">consulta de Hello, a continuación, se pasa toohello tooretrieve de servidor de base de datos de Cosmos un conjunto de resultados en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="fb4bf-798">Hola devuelve resultados son deserializados en un flujo de objetos de .NET en el lado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Arquitectura de consultas compatibles con LINQ que usa la API de DocumentDB: sintaxis SQL, lenguaje de consulta JSON, conceptos de base de datos y consultas SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="fb4bf-800">Asignación de .NET y JSON</span><span class="sxs-lookup"><span data-stu-id="fb4bf-800">.NET and JSON mapping</span></span>
<span data-ttu-id="fb4bf-801">asignación de Hello entre objetos .NET y documentos JSON es natural: se asigna a cada campo de miembro de datos tooa: objeto JSON, donde es el nombre del campo Hola asigna toohello "claves" parte del objeto de Hola y parte de "value" Hola se asignan de forma recursiva toohello parte de valor de objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="fb4bf-802">Considere el siguiente ejemplo de Hola: objeto de familia de hello creado es documento JSON de toohello asignado tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="fb4bf-803">Y viceversa, documento JSON de hello es objeto de .NET de tooa de espera asignado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="fb4bf-804">**Clase de C#**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-804">**C# Class**</span></span>

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


<span data-ttu-id="fb4bf-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-805">**JSON**</span></span>  

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



### <a name="linq-toosql-translation"></a><span data-ttu-id="fb4bf-806">Traducción de tooSQL LINQ</span><span class="sxs-lookup"><span data-stu-id="fb4bf-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="fb4bf-807">proveedor de consultas de base de datos de Cosmos Hola realiza una mejor asignación de esfuerzo de una consulta LINQ en una consulta SQL de la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="fb4bf-808">Hola siguiendo la descripción, suponemos lector hello tiene un conocimiento básico de LINQ.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="fb4bf-809">En primer lugar, para el sistema de tipos de hello, se admiten todos los tipos primitivos de JSON: tipos numéricos, boolean, string y null.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="fb4bf-810">Solo se admiten estos tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-810">Only these JSON types are supported.</span></span> <span data-ttu-id="fb4bf-811">Hola siguientes expresiones escalares es compatibles.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="fb4bf-812">Valores constantes: estos incluyen valores constantes de tipos de datos primitivos de hello en tiempo de Hola Hola consulta se evalúa.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="fb4bf-813">Expresiones de índice de propiedad/matriz: estas expresiones hacen referencia toohello propiedad de un objeto o un elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="fb4bf-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n es una variable int</span><span class="sxs-lookup"><span data-stu-id="fb4bf-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="fb4bf-815">Expresiones aritméticas: entre estas se incluyen expresiones aritméticas comunes o valores numéricos y booleanos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="fb4bf-816">Para la lista completa de hello, consulte Especificación de SQL toohello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="fb4bf-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="fb4bf-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="fb4bf-818">Expresión de comparación de cadena - puede tratarse comparar un valor de cadena de constante de cadena valor toosome.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="fb4bf-819">mother.familyName == "Smith";    child.givenName == s; //s es una variable de cadena</span><span class="sxs-lookup"><span data-stu-id="fb4bf-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="fb4bf-820">Expresión de creación de objetos o matrices: estas expresiones devuelven un objeto de tipo de valor compuesto o tipo anónimo o una matriz de estos objetos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="fb4bf-821">Estos valores se pueden anidar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-821">These values can be nested.</span></span>
  
     <span data-ttu-id="fb4bf-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //un tipo anónimo con dos campos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="fb4bf-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="fb4bf-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="fb4bf-824"><a id="SupportedLinqOperators"></a>Lista de los operadores LINQ admitidos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="fb4bf-825">Esta es una lista de los operadores LINQ compatibles en proveedor LINQ de hello incluido con hello documentos .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="fb4bf-826">**Seleccione**: proyecciones traducen toohello SQL SELECT incluida la construcción de objetos</span><span class="sxs-lookup"><span data-stu-id="fb4bf-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="fb4bf-827">**Donde**: filtros traducir toohello WHERE de SQL y admite la traducción entre & &, || y!</span><span class="sxs-lookup"><span data-stu-id="fb4bf-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="fb4bf-828">operadores SQL toohello</span><span class="sxs-lookup"><span data-stu-id="fb4bf-828">toohello SQL operators</span></span>
* <span data-ttu-id="fb4bf-829">**SelectMany**: permite el desenredo de la cláusula JOIN de SQL de matrices toohello.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="fb4bf-830">Puede ser usado toochain/anidar expresiones toofilter en elementos de matriz</span><span class="sxs-lookup"><span data-stu-id="fb4bf-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="fb4bf-831">**OrderBy y OrderByDescending**: traduce tooORDER BY ascendente o descendente</span><span class="sxs-lookup"><span data-stu-id="fb4bf-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="fb4bf-832">Los operadores **Count**, **Sum**, **Min**, **Max** y **Average** para la agregación y sus equivalentes asincrónicos **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** y **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="fb4bf-833">**CompareTo**: traduce toorange comparaciones.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="fb4bf-834">Se usa frecuentemente para las cadenas, debido a que no son comparables en .NET.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="fb4bf-835">**Tomar**: traduce toohello TOP de SQL para limitar los resultados de una consulta</span><span class="sxs-lookup"><span data-stu-id="fb4bf-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="fb4bf-836">**Funciones matemáticas**: admite la traducción de. Abs, Acos, Asin de NET, Atan, Ceiling, Cos, Exp, Floor, registro, Log10, Pow, Round, inicio de sesión, Sin, Sqrt, Tan, truncar funciones integradas de toohello equivalente de SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fb4bf-837">**Funciones de cadena**: admite la traducción de. Concat, Contains, EndsWith de NET, IndexOf, recuento, ToLower, TrimStart, Replace, inversa, TrimEnd, StartsWith, SubString, ToUpper toohello equivalente funciones integradas de SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fb4bf-838">**Funciones de matriz**: admite la traducción de. Concat, Contains y recuento toohello equivalente SQL funciones integradas de NET.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fb4bf-839">**Funciones de extensión geoespaciales**: admite la traducción de los métodos de código auxiliar distancia, en IsValid y IsValidDetailed toohello equivalente funciones integradas de SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fb4bf-840">**Extensión de la función definida por el usuario**: traducción admite de hello UserDefinedFunctionProvider.Invoke toohello correspondiente definido por el usuario función del método de código auxiliar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="fb4bf-841">**Varios**: admite la traducción de hello coalesce y operadores condicionales.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="fb4bf-842">Puede traducir Contains tooString CONTAINS, ARRAY_CONTAINS o hello IN de SQL según el contexto.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="fb4bf-843">Operadores de consulta SQL</span><span class="sxs-lookup"><span data-stu-id="fb4bf-843">SQL query operators</span></span>
<span data-ttu-id="fb4bf-844">Estos son algunos ejemplos que ilustran cómo algunos operadores de consulta LINQ estándar Hola se traducen las consultas de base de datos de tooCosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="fb4bf-845">Operador Select</span><span class="sxs-lookup"><span data-stu-id="fb4bf-845">Select Operator</span></span>
<span data-ttu-id="fb4bf-846">sintaxis de Hello es `input.Select(x => f(x))`, donde `f` es una expresión escalar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="fb4bf-847">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="fb4bf-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="fb4bf-849">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="fb4bf-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="fb4bf-851">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="fb4bf-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="fb4bf-853">Operador SelectMany</span><span class="sxs-lookup"><span data-stu-id="fb4bf-853">SelectMany operator</span></span>
<span data-ttu-id="fb4bf-854">sintaxis de Hello es `input.SelectMany(x => f(x))`, donde `f` es una expresión escalar que devuelve un tipo de colección.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="fb4bf-855">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="fb4bf-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="fb4bf-857">Operador Where</span><span class="sxs-lookup"><span data-stu-id="fb4bf-857">Where operator</span></span>
<span data-ttu-id="fb4bf-858">sintaxis de Hello es `input.Where(x => f(x))`, donde `f` es una expresión escalar, que devuelve un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="fb4bf-859">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="fb4bf-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="fb4bf-861">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="fb4bf-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="fb4bf-863">Composición de consultas SQL</span><span class="sxs-lookup"><span data-stu-id="fb4bf-863">Composite SQL queries</span></span>
<span data-ttu-id="fb4bf-864">Hola por encima de los operadores puede ser compuesto tooform consultas más eficaces.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="fb4bf-865">Puesto que la base de datos de Cosmos admite colecciones anidadas, composición Hola puede concatenar o anidado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="fb4bf-866">Concatenación</span><span class="sxs-lookup"><span data-stu-id="fb4bf-866">Concatenation</span></span>
<span data-ttu-id="fb4bf-867">sintaxis de Hello es `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="fb4bf-868">Una consulta concatenada puede empezar por una consulta `SelectMany` opcional seguida de varios operadores `Select` o `Where`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="fb4bf-869">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="fb4bf-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="fb4bf-871">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="fb4bf-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="fb4bf-873">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="fb4bf-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="fb4bf-875">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="fb4bf-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="fb4bf-877">Anidamiento</span><span class="sxs-lookup"><span data-stu-id="fb4bf-877">Nesting</span></span>
<span data-ttu-id="fb4bf-878">sintaxis de Hello es `input.SelectMany(x=>x.Q())` donde Q es un `Select`, `SelectMany`, o `Where` operador.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="fb4bf-879">En una consulta anidada, consulta interna de hello es aplicado tooeach elemento de colección exterior Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="fb4bf-880">Una característica importante es que esa consulta interna Hola puede hacer referencia toohello campos de elementos de Hola de colección exterior de hello como autocombinaciones.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="fb4bf-881">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="fb4bf-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="fb4bf-883">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="fb4bf-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="fb4bf-885">**Expresión lambda de LINQ**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="fb4bf-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="fb4bf-887"><a id="ExecutingSqlQueries"></a>Ejecución de consultas SQL</span><span class="sxs-lookup"><span data-stu-id="fb4bf-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="fb4bf-888">Cosmos DB expone recursos mediante la API de REST, que puede invocar cualquier lenguaje capaz de realizar solicitudes de HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="fb4bf-889">Además, Cosmos DB ofrece bibliotecas de programación para varios lenguajes populares como .NET, Node.js, JavaScript y Python.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="fb4bf-890">API de REST de Hola y Hola todas las distintas bibliotecas admiten consultas a través de SQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="fb4bf-891">Hola .NET SDK es compatible con LINQ asimismo consultar tooSQL.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="fb4bf-892">Hola siguientes ejemplos se muestra cómo toocreate una consulta y enviarlo en una cuenta de base de datos de la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="fb4bf-893"><a id="RestAPI"></a>API DE REST</span><span class="sxs-lookup"><span data-stu-id="fb4bf-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="fb4bf-894">Cosmos DB ofrece un modelo de programación RESTful sobre HTTP.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="fb4bf-895">Las cuentas de la base de datos pueden aprovisionarse usando una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="fb4bf-896">modelo de recursos de base de datos de Cosmos Hola consta de un conjunto de recursos en una cuenta de base de datos, cada uno de los cuales es direccionable mediante un URI lógico y estable.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="fb4bf-897">Un conjunto de recursos es tooas que se hace referencia una fuente de distribución en este documento.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="fb4bf-898">Una cuenta de la base de datos consta de un conjunto de bases de datos, cada una incluyendo varias recopilaciones que, a su vez, contienen documentos, UDF y otros tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="fb4bf-899">modelo de interacción básica Hello con estos recursos es a través de verbos de hello HTTP GET, PUT, POST y DELETE con su interpretación estándar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="fb4bf-900">verbo POST de Hola se utiliza para la creación de un nuevo recurso, para ejecutar un procedimiento almacenado o para emitir una consulta de base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="fb4bf-901">Las consultas siempre son operaciones de solo lectura sin efectos secundarios.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="fb4bf-902">Hello en los ejemplos siguientes muestran una entrada para una consulta de DocumentDB API realizada en una colección que contiene dos documentos de ejemplo Hola que hemos visto hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="fb4bf-903">consulta de Hello tiene un filtro simple en la propiedad de nombre de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="fb4bf-904">Tenga en cuenta use Hola de hello `x-ms-documentdb-isquery` y Content-Type: `application/query+json` toodenote encabezados que Hola operación es una consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="fb4bf-905">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-905">**Request**</span></span>

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


<span data-ttu-id="fb4bf-906">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-906">**Results**</span></span>

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


<span data-ttu-id="fb4bf-907">Hola segundo ejemplo muestra una consulta más compleja que devuelve varios resultados de la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="fb4bf-908">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-908">**Request**</span></span>

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


<span data-ttu-id="fb4bf-909">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="fb4bf-909">**Results**</span></span>

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


<span data-ttu-id="fb4bf-910">Si los resultados de una consulta no caben dentro de una sola página de resultados, Hola REST API devuelve un token de continuación a través de hello `x-ms-continuation-token` encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="fb4bf-911">Los clientes pueden paginar resultados mediante la inclusión de encabezado de hello en los resultados siguientes.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="fb4bf-912">número de Hola de resultados por página también puede controlarse mediante hello `x-ms-max-item-count` encabezado de número.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="fb4bf-913">Si la consulta especificada de hello tiene una función de agregación como `COUNT`, a continuación, la página de consulta de hello puede devolver un valor parcial agregado a través de la página de Hola de resultados.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="fb4bf-914">los clientes de Hello debe realizar una agregación de segundo nivel a través de estos resultados tooproduce Hola resultados finales, por ejemplo, sumar los recuentos de hello devueltos en el recuento total de hello páginas individuales tooreturn Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="fb4bf-915">Directiva de coherencia de datos toomanage Hola para las consultas, use hello `x-ms-consistency-level` encabezado al igual que todas las solicitudes de API de REST.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="fb4bf-916">Para mantener la coherencia sesión, es necesario tooalso Hola de eco más reciente `x-ms-session-token` encabezado de Cookie de solicitud de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="fb4bf-917">Hello directiva de indexación consultado la colección también puede influir coherencia Hola de resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="fb4bf-918">No tiene valor predeterminado de hello indización de configuración de directiva, para las colecciones Hola índice siempre está actual con el contenido del documento de Hola y consulta los resultados coincidan con coherencia de hello elegido para los datos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="fb4bf-919">Si hello directiva de indexación es tooLazy flexible, las consultas pueden devolver resultados obsoletos.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="fb4bf-920">Para más información, vea [Niveles de coherencia en Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="fb4bf-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="fb4bf-921">Si la directiva de indexación de hello configurado en la colección de hello no es compatible con la consulta especificada de hello, servidor de base de datos de Azure Cosmos Hola devuelve 400 "solicitud incorrecta".</span><span class="sxs-lookup"><span data-stu-id="fb4bf-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="fb4bf-922">Esto se devuelve para las consultas por rango en rutas de acceso configuradas para búsquedas hash (igualdad) y rutas de acceso excluidas de forma explícita de los índices.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="fb4bf-923">Hola `x-ms-documentdb-query-enable-scan` encabezado puede ser especificado tooallow Hola consulta tooperform un examen cuando un índice no está disponible.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="fb4bf-924">Puede obtener métricas detalladas en ejecución de la consulta estableciendo `x-ms-documentdb-populatequerymetrics` encabezado demasiado`True`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="fb4bf-925">Para más información, vea, [Métricas de consulta de SQL para la API de DocumentDB de Azure Cosmos DB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fb4bf-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="fb4bf-926"><a id="DotNetSdk"></a>SDK de C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="fb4bf-927">Hola .NET SDK es compatible con LINQ y SQL consultar.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="fb4bf-928">Hello en el ejemplo siguiente se muestra la consulta de filtro simple hello tooperform introdujo anteriormente en este documento.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="fb4bf-929">En este ejemplo se comparan dos propiedades para igualdad en cada documento y se usan proyecciones anónimas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="fb4bf-930">Hola siguiente muestra las combinaciones, expresadas a través de LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="fb4bf-931">cliente de .NET de Hello automáticamente recorre en iteración todas las páginas de Hola de resultados de la consulta en los bloques de foreach hello como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="fb4bf-932">consulta Hola opciones que se presentan en la sección de la API de REST de hello también están disponibles en Hola SDK de .NET con hello `FeedOptions` y `FeedResponse` las clases de hello CreateDocumentQuery método.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="fb4bf-933">número de Hola de páginas puede controlarse mediante hello `MaxItemCount` configuración.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="fb4bf-934">Puede controlar explícitamente la paginación mediante la creación de `IDocumentQueryable` con hello `IQueryable` objeto, a continuación, al leer la` ResponseContinuationToken` valores y pasándolos nuevo como `RequestContinuationToken` en `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="fb4bf-935">`EnableScanInQuery`puede ser el conjunto tooenable exámenes cuando no se admite la consulta Hola por directiva de indexación de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="fb4bf-936">Para las colecciones particionadas, puede usar `PartitionKey` toorun consulta de hello en una sola partición (aunque Cosmos DB puede extraer automáticamente esto de texto de la consulta de hello), y `EnableCrossPartitionQuery` ejecutan consultas de toorun que necesitan toobe en varias particiones.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="fb4bf-937">Consulte demasiado[ejemplos de .NET de base de datos de Azure Cosmos](https://github.com/Azure/azure-documentdb-net) para ver más ejemplos que contienen consultas.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="fb4bf-938"><a id="JavaScriptServerSideApi"></a>API del servidor de JavaScript</span><span class="sxs-lookup"><span data-stu-id="fb4bf-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="fb4bf-939">COSMOS DB proporciona un modelo de programación para ejecutar lógica de la aplicación de JavaScript que se basa directamente en las colecciones de hello mediante procedimientos almacenados y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="fb4bf-940">lógica de JavaScript de Hello registrado en el nivel de colección, a continuación, puede emitir las operaciones de base de datos en operaciones de hello en documentos de Hola de hello dado de la colección.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="fb4bf-941">Estas operaciones se incluyen en transacciones ACID ambientales.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="fb4bf-942">Hello en el ejemplo siguiente se muestra cómo las consultas toouse hello queryDocuments en toomake Hola API de servidor de JavaScript desde dentro de procedimientos almacenados y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

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

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="fb4bf-943"><a id="References"></a>Referencias</span><span class="sxs-lookup"><span data-stu-id="fb4bf-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="fb4bf-944">[Introducción tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="fb4bf-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="fb4bf-945">Especificación de SQL de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb4bf-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="fb4bf-946">Ejemplos de .NET de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb4bf-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="fb4bf-947">[Niveles de coherencia de Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="fb4bf-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="fb4bf-948">SQL ANSI 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="fb4bf-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="fb4bf-950">Especificación de JavaScript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="fb4bf-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="fb4bf-952">Técnicas de evaluación de consultas para bases de datos de gran tamaño [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="fb4bf-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="fb4bf-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="fb4bf-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="fb4bf-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="fb4bf-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="fb4bf-956">G.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-956">G.</span></span> <span data-ttu-id="fb4bf-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-957">Graefe.</span></span> <span data-ttu-id="fb4bf-958">marco de cascadas de Hola para optimizar la consulta.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="fb4bf-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-959">IEEE Data Eng.</span></span> <span data-ttu-id="fb4bf-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="fb4bf-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md