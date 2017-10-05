---
title: "Programación de JavaScript en el lado del servidor de Azure Cosmos DB | Microsoft Docs"
description: "Obtenga información sobre cómo usar Azure Cosmos DB para escribir procedimientos almacenados, desencadenadores de base de datos y funciones definidas por el usuario en JavaScript. Obtenga sugerencias de programación de base de datos y mucho más."
keywords: Desencadenadores de base de datos, procedimiento almacenado, procedimiento almacenado, programa de base de datos, sproc, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="bb149-105">Programación en el servidor de Azure Cosmos DB: procedimientos almacenados, desencadenadores de base de datos y funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="bb149-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="bb149-106">Conozca cómo la ejecución transaccional integrada del lenguaje de Azure Cosmos DB de JavaScript permite a los desarrolladores escribir **procedimientos almacenados**, **desencadenadores** y **funciones definidas por el usuario (UDF)** de forma nativa en un elemento de JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/).</span><span class="sxs-lookup"><span data-stu-id="bb149-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="bb149-107">Esto permite escribir la lógica de aplicación del programa de base de datos que se puede enviar y ejecutar directamente en las particiones de almacenamiento de base de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="bb149-108">Se recomienda comenzar con el vídeo siguiente, en el que Andrew Liu ofrece una breve introducción al modelo de programación de base de datos en el servidor de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="bb149-109">A continuación, vuelva a este artículo, donde conocerá las respuestas a las preguntas siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb149-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="bb149-110">¿Cómo se escribe un procedimiento almacenado, un desencadenador o una UDF con JavaScript?</span><span class="sxs-lookup"><span data-stu-id="bb149-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="bb149-111">¿Qué garantías ACID ofrece Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="bb149-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="bb149-112">¿Cómo funcionan las transacciones en Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="bb149-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="bb149-113">¿Qué son los desencadenadores previos y posteriores y cómo se escriben?</span><span class="sxs-lookup"><span data-stu-id="bb149-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="bb149-114">¿Cómo se registran y se ejecutan un procedimiento almacenado, un desencadenador o una UDF de forma compatible con REST mediante HTTP?</span><span class="sxs-lookup"><span data-stu-id="bb149-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="bb149-115">¿Qué SDK de Cosmos DB está disponible para crear y ejecutar procedimientos almacenados, desencadenadores y funciones definidas por el usuario?</span><span class="sxs-lookup"><span data-stu-id="bb149-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="bb149-116">Introducción a la programación con UDF y procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="bb149-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="bb149-117">Este enfoque de *"JavaScript como un T-SQL moderno"* libera a los desarrolladores de aplicaciones de las complejidades de los errores de coincidencia del sistema de tipo y de las tecnologías de asignación relacional de objetos.</span><span class="sxs-lookup"><span data-stu-id="bb149-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="bb149-118">También cuenta con un número de ventajas intrínsecas que se pueden utilizar para generar sofisticadas aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="bb149-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="bb149-119">**Lógica de procedimientos:** JavaScript como un lenguaje de programación de alto nivel, proporciona una interfaz completa y familiar para expresar la lógica empresarial.</span><span class="sxs-lookup"><span data-stu-id="bb149-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="bb149-120">Puede realizar secuencias complejas de operaciones acercándose más a los datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="bb149-121">**Transacciones atómicas:** Cosmos DB garantiza que las operaciones de base de datos realizadas dentro de un único procedimiento almacenado o desencadenador sean atómicas.</span><span class="sxs-lookup"><span data-stu-id="bb149-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="bb149-122">Esto permite a una aplicación combinar operaciones relacionadas en un único lote para que todas se realicen correctamente o no lo haga ninguna.</span><span class="sxs-lookup"><span data-stu-id="bb149-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="bb149-123">**Rendimiento**: el hecho de que JSON se asigne intrínsecamente al sistema de tipo de lenguaje de Javascript y que también sea la unidad básica de almacenamiento en Cosmos DB permite un número de optimizaciones como la materialización diferida de documentos JSON en el grupo de búferes y hacerlos disponibles bajo demanda para el código de ejecución.</span><span class="sxs-lookup"><span data-stu-id="bb149-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="bb149-124">Hay más ventajas de rendimiento asociadas con el envío de la lógica empresarial a la base de datos:</span><span class="sxs-lookup"><span data-stu-id="bb149-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="bb149-125">Procesamiento por lotes: los desarrolladores pueden agrupar operaciones como inserciones y enviarlas en masa.</span><span class="sxs-lookup"><span data-stu-id="bb149-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="bb149-126">El coste de la latencia de tráfico de red y la sobrecarga de almacenamiento para crear transacciones independientes se reducen de forma significativa.</span><span class="sxs-lookup"><span data-stu-id="bb149-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="bb149-127">Precompilación: Cosmos DB precompila procedimientos almacenados, desencadenadores y funciones definidas por el usuario para evitar el coste de compilación de JavaScript en cada invocación.</span><span class="sxs-lookup"><span data-stu-id="bb149-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="bb149-128">La sobrecarga de generar el código de byte para la lógica de procedimiento se amortiza en un valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="bb149-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="bb149-129">Secuenciación: muchas operaciones necesitan un efecto secundario (“desencadenador”) que implica potencialmente realizar una o más operaciones de almacenamiento secundarias.</span><span class="sxs-lookup"><span data-stu-id="bb149-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="bb149-130">Aparte de la atomicidad, tiene mayor rendimiento cuando se mueve al servidor.</span><span class="sxs-lookup"><span data-stu-id="bb149-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="bb149-131">**Encapsulación:** los procedimientos almacenados se pueden utilizar para agrupar la lógica empresarial en un lugar.</span><span class="sxs-lookup"><span data-stu-id="bb149-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="bb149-132">Esto tiene dos ventajas:</span><span class="sxs-lookup"><span data-stu-id="bb149-132">This has two advantages:</span></span>
  * <span data-ttu-id="bb149-133">Agrega una capa de abstracción en la parte superior de los datos sin procesar, lo cual permite a los arquitectos de datos desarrollar sus aplicaciones de forma independiente de los datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="bb149-134">Esto supone una especial ventaja cuando los datos no tienen esquema, debido a débiles suposiciones que se deben integrar en la aplicación si tienen que tratar directamente con los datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="bb149-135">Esta abstracción permite a las empresas mantener seguros sus datos simplificando el acceso desde los scripts.</span><span class="sxs-lookup"><span data-stu-id="bb149-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="bb149-136">Se admite la creación y ejecución de operadores de consulta personalizados, procedimientos almacenados y desencadenadores de base de datos mediante la [API de REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) y los [SDK de cliente](documentdb-sdk-dotnet.md) de muchas plataformas, como .NET, Node.js y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bb149-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="bb149-137">En este tutorial se usa el [SDK de Node.js con objetos Q promise](http://azure.github.io/azure-documentdb-node-q/) para mostrar la sintaxis y el uso de procedimientos almacenados, desencadenadores y funciones definidas por el usuario (UDF).</span><span class="sxs-lookup"><span data-stu-id="bb149-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="bb149-138">Procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="bb149-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="bb149-139">Ejemplo: creación de un procedimiento almacenado sencillo</span><span class="sxs-lookup"><span data-stu-id="bb149-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="bb149-140">Comencemos con un sencillo procedimiento almacenado que devuelve una respuesta “Hello World”.</span><span class="sxs-lookup"><span data-stu-id="bb149-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="bb149-141">Los procedimientos almacenados se registran por colección y pueden funcionar en cualquier documento y dato adjunto presente en esa colección.</span><span class="sxs-lookup"><span data-stu-id="bb149-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="bb149-142">En el siguiente fragmento se muestra cómo registrar el procedimiento almacenado Hola mundo con una colección.</span><span class="sxs-lookup"><span data-stu-id="bb149-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="bb149-143">Una vez que se registre el procedimiento almacenado, podemos ejecutarlo con la colección y leer los resultados en el cliente.</span><span class="sxs-lookup"><span data-stu-id="bb149-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="bb149-144">El objeto de contexto proporciona acceso a todas las operaciones que se pueden realizar en el almacenamiento de Cosmos DB, así como acceso a los objetos de solicitud y respuesta.</span><span class="sxs-lookup"><span data-stu-id="bb149-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="bb149-145">En este caso, hemos utilizado el objeto de respuesta para establecer el cuerpo de la respuesta que se ha devuelto al cliente.</span><span class="sxs-lookup"><span data-stu-id="bb149-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="bb149-146">Para más información, consulte la [documentación del SDK del lado del servidor JavaScript de Azure Cosmos DB](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="bb149-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="bb149-147">Permítanos ampliar este ejemplo y agregar más funcionalidad relacionada con la base de datos al procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="bb149-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="bb149-148">Los procedimientos almacenados pueden crear, actualizar, leer, consultar y eliminar documentos y datos adjuntos de la colección.</span><span class="sxs-lookup"><span data-stu-id="bb149-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="bb149-149">Ejemplo: escritura de un procedimiento almacenado para crear un documento</span><span class="sxs-lookup"><span data-stu-id="bb149-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="bb149-150">En el siguiente fragmento, se muestra cómo utilizar el objeto de contexto para que interactúe con los recursos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="bb149-151">Este procedimiento almacenado toma como entrada documentToCreate, el cuerpo de un documento que se va a crear en la colección actual.</span><span class="sxs-lookup"><span data-stu-id="bb149-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="bb149-152">Todas estas operaciones son asíncronas y dependen de las devoluciones de llamadas de función de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bb149-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="bb149-153">La función de devolución de llamada tiene dos parámetros, uno para el objeto de error en caso de que falle la operación y otro para el objeto creado.</span><span class="sxs-lookup"><span data-stu-id="bb149-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="bb149-154">Dentro de la devolución de llamada, los usuarios pueden controlar la excepción o lanzar un error.</span><span class="sxs-lookup"><span data-stu-id="bb149-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="bb149-155">En caso de que no se proporcione una devolución de llamada y haya un error, el sistema en tiempo de ejecución de Azure Cosmos DB produce un error.</span><span class="sxs-lookup"><span data-stu-id="bb149-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="bb149-156">En el ejemplo anterior, la devolución de llamada lanza un error si falló la operación.</span><span class="sxs-lookup"><span data-stu-id="bb149-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="bb149-157">De lo contrario, establece el identificador del documento creado como el cuerpo de la respuesta al cliente.</span><span class="sxs-lookup"><span data-stu-id="bb149-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="bb149-158">A continuación se explica cómo se ejecuta este procedimiento almacenado con parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb149-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="bb149-159">Tenga en cuenta que este procedimiento almacenado se puede modificar para tomar una matriz de cuerpos de documentos como la entrada y crearlos todos en la misma ejecución del procedimiento almacenado en lugar de en varias solicitudes de red para crear cada uno individualmente.</span><span class="sxs-lookup"><span data-stu-id="bb149-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="bb149-160">Esto se puede utilizar para implementar un importador masivo eficiente para Cosmos DB, algo que se tratará más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bb149-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="bb149-161">El ejemplo descrito ha demostrado cómo utilizar procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="bb149-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="bb149-162">Más tarde trataremos los desencadenadores y las funciones definidas por el usuario (UDF) en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="bb149-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="bb149-163">Transacciones del programa de base de datos</span><span class="sxs-lookup"><span data-stu-id="bb149-163">Database program transactions</span></span>
<span data-ttu-id="bb149-164">Una transacción en una base de datos típica se puede definir como una secuencia de operaciones realizadas como una única unidad lógica de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb149-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="bb149-165">Cada transacción proporciona **garantías ACID**.</span><span class="sxs-lookup"><span data-stu-id="bb149-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="bb149-166">ACID es un acrónimo conocido que, por sus siglas en inglés, hace referencia a cuatro propiedades: Atomicidad, Coherencia, Aislamiento y Durabilidad.</span><span class="sxs-lookup"><span data-stu-id="bb149-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="bb149-167">Brevemente, la atomicidad garantiza que todo el trabajo realizado dentro de una transacción se lea como una única unidad donde se confirma todo o nada.</span><span class="sxs-lookup"><span data-stu-id="bb149-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="bb149-168">La Coherencia asegura que los datos se encuentran siempre en buen estado interno en todas las transacciones.</span><span class="sxs-lookup"><span data-stu-id="bb149-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="bb149-169">El Aislamiento garantiza que dos transacciones no pueden interferir entre ellas; generalmente, la mayoría de los sistemas comerciales proporcionan varios niveles de aislamiento que se pueden utilizar según las necesidades de aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb149-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="bb149-170">La Durabilidad asegura que cualquier cambio que esté confirmado en la base de datos estará siempre presente.</span><span class="sxs-lookup"><span data-stu-id="bb149-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="bb149-171">En Cosmos DB, JavaScript está hospedado en el mismo espacio de memoria que la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="bb149-172">Por lo tanto, las solicitudes realizadas dentro de los procedimientos almacenados y desencadenadores se ejecutan en el mismo ámbito de una sesión de base de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="bb149-173">Esto permite a Cosmos DB garantizar ACID para todas las operaciones que formen parte de un único procedimiento almacenado/desencadenador.</span><span class="sxs-lookup"><span data-stu-id="bb149-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="bb149-174">Considere la siguiente definición de procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="bb149-174">Consider the following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="bb149-175">Este procedimiento almacenado utiliza transacciones con una aplicación de juegos para intercambiar elementos entre dos jugadores en una única operación.</span><span class="sxs-lookup"><span data-stu-id="bb149-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="bb149-176">El procedimiento almacenado intenta leer dos documentos, cada uno de ellos corresponde al identificador del jugador que se ha pasado como un argumento.</span><span class="sxs-lookup"><span data-stu-id="bb149-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="bb149-177">Si se encuentran ambos documentos de jugador, entonces el procedimiento almacenado actualiza los documentos intercambiando sus elementos.</span><span class="sxs-lookup"><span data-stu-id="bb149-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="bb149-178">Si se produce cualquier error durante el proceso, lanza una excepción de JavaScript que de forma implícita cancela la transacción.</span><span class="sxs-lookup"><span data-stu-id="bb149-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="bb149-179">Si la colección en la que se encuentra registrado el procedimiento almacenado es de partición única, la transacción estará en el ámbito de todos los documentos de la colección.</span><span class="sxs-lookup"><span data-stu-id="bb149-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="bb149-180">Si la colección tiene particiones, los procedimientos almacenados se ejecutan en el ámbito de transacción de una clave de partición única.</span><span class="sxs-lookup"><span data-stu-id="bb149-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="bb149-181">Por tanto, cada ejecución de procedimientos almacenados debe incluir un valor de clave de partición que se corresponda con el ámbito en que debe ejecutarse la transacción.</span><span class="sxs-lookup"><span data-stu-id="bb149-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="bb149-182">Para más información, consulte [Creación de particiones con Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="bb149-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="bb149-183">Confirmación y reversión</span><span class="sxs-lookup"><span data-stu-id="bb149-183">Commit and rollback</span></span>
<span data-ttu-id="bb149-184">Las transacciones están integradas de forma profunda y nativa en el modelo de programación de JavaScript de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="bb149-185">Dentro de una función de JavaScript, todas las operaciones se ajustan automáticamente en una única transacción.</span><span class="sxs-lookup"><span data-stu-id="bb149-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="bb149-186">Si el JavaScript se completa sin excepciones, se confirman las operaciones en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="bb149-187">De hecho, las instrucciones “BEGIN TRANSACTION” y “COMMIT TRANSACTION” en las bases de datos relacionales están implícitas en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="bb149-188">Si existe cualquier excepción que se propague desde el script, el sistema en tiempo de ejecución de JavaScript de Cosmos DB revertirá toda la transacción.</span><span class="sxs-lookup"><span data-stu-id="bb149-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="bb149-189">Como se muestra en el ejemplo anterior, iniciar una excepción es un equivalente efectivo de “ROLLBACK TRANSACTION” en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="bb149-190">Coherencia de datos</span><span class="sxs-lookup"><span data-stu-id="bb149-190">Data consistency</span></span>
<span data-ttu-id="bb149-191">Los procedimientos almacenados y los desencadenadores se ejecutan siempre en la réplica principal del contenedor de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="bb149-192">Esto garantiza que las lecturas desde dentro de los procedimientos almacenados ofrecen una fuerte coherencia.</span><span class="sxs-lookup"><span data-stu-id="bb149-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="bb149-193">Las consultas que utilizan funciones definidas por el usuario se pueden ejecutar en la réplica principal o en cualquier réplica secundaria, pero nos aseguramos de cumplir con el nivel de coherencia solicitado seleccionando la réplica adecuada.</span><span class="sxs-lookup"><span data-stu-id="bb149-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="bb149-194">Ejecución vinculada</span><span class="sxs-lookup"><span data-stu-id="bb149-194">Bounded execution</span></span>
<span data-ttu-id="bb149-195">Todas las operaciones de Cosmos DB se deben completar dentro de la duración del tiempo de espera de la solicitud especificada.</span><span class="sxs-lookup"><span data-stu-id="bb149-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="bb149-196">Esta restricción también se aplica a las funciones de JavaScript (procedimientos almacenados, desencadenadores y funciones definidas por el usuario).</span><span class="sxs-lookup"><span data-stu-id="bb149-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="bb149-197">Si una operación no se completa dentro de ese límite de tiempo, la transacción se revierte.</span><span class="sxs-lookup"><span data-stu-id="bb149-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="bb149-198">Las funciones de JavaScript deben finalizar dentro del límite de tiempo o implementar un modelo basado en la continuación en el lote o reanudar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="bb149-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="bb149-199">Con el fin de simplificar el desarrollo de los procedimientos almacenados y los desencadenadores para controlar los límites de tiempo, todas las funciones del objeto de colección (para crear, leer, reemplazar y eliminar documentos y datos adjuntos) devuelven un valor booleano que representa si se completará la operación.</span><span class="sxs-lookup"><span data-stu-id="bb149-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="bb149-200">Si este valor es falso, es un indicador de que el límite de tiempo está a punto de cumplirse y de que el procedimiento debe concluir la ejecución.</span><span class="sxs-lookup"><span data-stu-id="bb149-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="bb149-201">Se garantiza la finalización de las operaciones en cola anteriores a la primera operación de almacenamiento no aceptada si el procedimiento almacenado se completa a tiempo y no pone en cola más solicitudes.</span><span class="sxs-lookup"><span data-stu-id="bb149-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="bb149-202">Las funciones de JavaScript también se vinculan al consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb149-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="bb149-203">Cosmos DB reserva la capacidad de proceso por colección en función del tamaño aprovisionado de una cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="bb149-204">La capacidad de proceso se expresa en términos de una unidad de CPU normalizada, consumo de memoria y E/S llamadas unidades de solicitud o RU.</span><span class="sxs-lookup"><span data-stu-id="bb149-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="bb149-205">Las funciones de JavaScript pueden utilizar potencialmente un gran número de RU en poco tiempo y podrían obtener una limitación de frecuencia si se alcanza el límite de la colección.</span><span class="sxs-lookup"><span data-stu-id="bb149-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="bb149-206">Los procedimientos almacenados que utilizan muchos recursos también podrían ponerse en cuarentena para garantizar la disponibilidad de operaciones de base de datos primitivas.</span><span class="sxs-lookup"><span data-stu-id="bb149-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="bb149-207">Ejemplo: importación masiva de datos a un programa de base de datos</span><span class="sxs-lookup"><span data-stu-id="bb149-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="bb149-208">A continuación se muestra un ejemplo de un procedimiento almacenado que se escribe en documentos de importación masiva de una colección.</span><span class="sxs-lookup"><span data-stu-id="bb149-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="bb149-209">Observe cómo controla el procedimiento almacenado la ejecución vinculada comprobando el valor de devolución booleano de createDocument y, a continuación, utiliza el recuento de documentos insertados en cada invocación del procedimiento almacenado para realizar un seguimiento y reanudar el progreso en todos los lotes.</span><span class="sxs-lookup"><span data-stu-id="bb149-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="bb149-210"><a id="trigger"></a> Desencadenadores de base de datos</span><span class="sxs-lookup"><span data-stu-id="bb149-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="bb149-211">Desencadenadores previos de base de datos</span><span class="sxs-lookup"><span data-stu-id="bb149-211">Database pre-triggers</span></span>
<span data-ttu-id="bb149-212">Cosmos DB proporciona desencadenadores que se ejecutan o desencadenan por una operación en un documento.</span><span class="sxs-lookup"><span data-stu-id="bb149-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="bb149-213">Por ejemplo, puede especificar un desencadenador previo al crear un documento; este desencadenador previo se ejecutará antes de crear el documento.</span><span class="sxs-lookup"><span data-stu-id="bb149-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="bb149-214">A continuación se muestra un ejemplo de cómo se pueden utilizar desencadenadores previos para validar las propiedades de un documento que se está creando:</span><span class="sxs-lookup"><span data-stu-id="bb149-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="bb149-215">Y el código de registro del cliente de Node.js correspondiente para el desencadenador:</span><span class="sxs-lookup"><span data-stu-id="bb149-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="bb149-216">Los desencadenadores previos no pueden tener parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb149-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="bb149-217">El objeto solicitado se puede utilizar para manipular el mensaje de solicitud asociado con la operación.</span><span class="sxs-lookup"><span data-stu-id="bb149-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="bb149-218">Aquí, el desencadenador previo se está ejecutando con la creación de un documento y el cuerpo del mensaje de solicitud contiene el documento que se va a crear en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="bb149-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="bb149-219">Cuando se registran los desencadenadores, los usuarios pueden especificar las operaciones que se pueden ejecutar con ellos.</span><span class="sxs-lookup"><span data-stu-id="bb149-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="bb149-220">Este desencadenador se ha creado con TriggerOperation.Create, lo que significa que no se permite lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="bb149-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="bb149-221">Desencadenadores anteriores de base de datos</span><span class="sxs-lookup"><span data-stu-id="bb149-221">Database post-triggers</span></span>
<span data-ttu-id="bb149-222">Los desencadenadores posteriores, del mismo modo que los previos, se asocian con una operación de un documento y no aceptan parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb149-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="bb149-223">Se ejecutan **después** de que se haya completado la operación y tienen acceso al mensaje de respuesta que se envía al cliente.</span><span class="sxs-lookup"><span data-stu-id="bb149-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="bb149-224">El siguiente ejemplo muestra desencadenadores posteriores en acción:</span><span class="sxs-lookup"><span data-stu-id="bb149-224">The following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="bb149-225">El desencadenador se puede registrar como se muestra en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bb149-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="bb149-226">Este desencadenador consulta el documento de metadatos y lo actualiza con detalles del documento recién creado.</span><span class="sxs-lookup"><span data-stu-id="bb149-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="bb149-227">Es importante tener en cuenta la ejecución **transaccional** de los desencadenadores en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="bb149-228">Este desencadenador posterior se ejecuta como parte de la misma transacción cuando se crea el documento original.</span><span class="sxs-lookup"><span data-stu-id="bb149-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="bb149-229">Por lo tanto, si lanzamos una excepción desde el desencadenador posterior (en caso de que no podamos actualizar el documento de metadatos), fallará y se revertirá toda la transacción.</span><span class="sxs-lookup"><span data-stu-id="bb149-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="bb149-230">No se creará ningún documento y se devolverá una excepción.</span><span class="sxs-lookup"><span data-stu-id="bb149-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="bb149-231"><a id="udf"></a>Funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="bb149-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="bb149-232">Las funciones definidas por el usuario se utilizan para ampliar la gramática del lenguaje de consultas SQL de la API de DocumentDB e implementar la lógica empresarial personalizada.</span><span class="sxs-lookup"><span data-stu-id="bb149-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="bb149-233">Solo se las puede llamar desde consultas internas.</span><span class="sxs-lookup"><span data-stu-id="bb149-233">They can only be called from inside queries.</span></span> <span data-ttu-id="bb149-234">No tienen acceso al objeto de contexto y se supone que se deben utilizar como un JavaScript únicamente de cálculo.</span><span class="sxs-lookup"><span data-stu-id="bb149-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="bb149-235">Por lo tanto, las funciones definidas por el usuario se pueden ejecutar en réplicas secundarias del servicio Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="bb149-236">En el siguiente ejemplo, se crea una UDF para calcular la base imponible basada en tipos para varios niveles de renta y, a continuación, se usa dentro de una consulta para buscar a todas las personas que pagan más de 20.000 $ en impuestos.</span><span class="sxs-lookup"><span data-stu-id="bb149-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="bb149-237">La UDF se puede utilizar de forma consecuente en consultas como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb149-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="bb149-238">API de consulta integradas en lenguajes JavaScript</span><span class="sxs-lookup"><span data-stu-id="bb149-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="bb149-239">Además de emitir consultas mediante la gramática de SQL del DocumentDB, el SDK del lado servidor permite realizar consultas optimizadas a través de una interfaz fluida de JavaScript sin necesitar conocimientos de SQL.</span><span class="sxs-lookup"><span data-stu-id="bb149-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="bb149-240">La API de consulta de JavaScript permite crear mediante programación las consultas al pasar las funciones de predicado a función encadenada, con una sintaxis familiar para los elementos integrados de matriz de ECMAScript5 y las bibliotecas populares de JavaScript, como lodash.</span><span class="sxs-lookup"><span data-stu-id="bb149-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="bb149-241">Las consultas se analizan con el tiempo de ejecución de JavaScript para que se ejecuten eficazmente mediante índices de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb149-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="bb149-242">`__` (subrayado doble) es un alias para `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="bb149-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="bb149-243">En otras palabras, puede utilizar `__` o `getContext().getCollection()` para obtener acceso a la API de consulta de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bb149-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="bb149-244">Estas son algunas de las funciones compatibles:</span><span class="sxs-lookup"><span data-stu-id="bb149-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="bb149-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-246">Inicia una llamada encadenada que debe terminarse con value().</span><span class="sxs-lookup"><span data-stu-id="bb149-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="bb149-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-248">Filtra la entrada usando una función de predicado que devuelve True o False para filtrar los documentos de entrada y salida en el conjunto resultante.</span><span class="sxs-lookup"><span data-stu-id="bb149-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="bb149-249">Este comportamiento es similar al de una cláusula WHERE de SQL.</span><span class="sxs-lookup"><span data-stu-id="bb149-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="bb149-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-251">Se aplica una proyección dado que se trata de una función de transformación que asigna cada elemento de entrada a un valor u objeto de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bb149-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="bb149-252">Este comportamiento es similar al de una cláusula SELECT de SQL.</span><span class="sxs-lookup"><span data-stu-id="bb149-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="bb149-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-254">Se trata de un acceso directo a una asignación que extrae el valor de una propiedad única de cada elemento de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb149-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="bb149-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-256">Combina y reduce las matrices de cada elemento de entrada en una sola matriz.</span><span class="sxs-lookup"><span data-stu-id="bb149-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="bb149-257">Este comportamiento es similar a SelectMany de LINQ.</span><span class="sxs-lookup"><span data-stu-id="bb149-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="bb149-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-259">Genera un nuevo conjunto de documentos al clasificarlos en orden ascendente en la secuencia de documentos de entrada según el predicado especificado.</span><span class="sxs-lookup"><span data-stu-id="bb149-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="bb149-260">Este comportamiento es similar al de una cláusula ORDER BY de SQL.</span><span class="sxs-lookup"><span data-stu-id="bb149-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="bb149-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="bb149-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="bb149-262">Genera un nuevo conjunto de documentos al clasificarlos en orden descendente en la secuencia de documentos de entrada según el predicado especificado.</span><span class="sxs-lookup"><span data-stu-id="bb149-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="bb149-263">Este comportamiento es similar al de una cláusula ORDER BY x DESC de SQL.</span><span class="sxs-lookup"><span data-stu-id="bb149-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="bb149-264">Cuando se incluye dentro del predicado o las funciones selectoras, las siguientes construcciones de JavaScript se optimizan automáticamente para ejecutarse directamente en índices de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="bb149-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="bb149-265">Operadores simples: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="bb149-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="bb149-266">Literales, incluido el literal de objeto: {}</span><span class="sxs-lookup"><span data-stu-id="bb149-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="bb149-267">var, return</span><span class="sxs-lookup"><span data-stu-id="bb149-267">var, return</span></span>

<span data-ttu-id="bb149-268">Las siguientes construcciones de JavaScript no se optimizan para índices de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="bb149-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="bb149-269">Control de flujo (por ejemplo: if, for, while)</span><span class="sxs-lookup"><span data-stu-id="bb149-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="bb149-270">Llamadas a funciones</span><span class="sxs-lookup"><span data-stu-id="bb149-270">Function calls</span></span>

<span data-ttu-id="bb149-271">Para obtener más información, consulte [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="bb149-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="bb149-272">Ejemplo: escribir un procedimiento almacenado mediante la API de consulta de JavaScript</span><span class="sxs-lookup"><span data-stu-id="bb149-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="bb149-273">El ejemplo de código siguiente es un ejemplo de cómo se puede usar la API de consulta de JavaScript en el contexto de un procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="bb149-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="bb149-274">El procedimiento almacenado inserta un documento, proporcionado por un parámetro de entrada y actualiza un documento de metadatos, mediante el método `__.filter()` , con los valores minSize, maxSize y totalSize basados en la propiedad de tamaño del documento de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb149-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="bb149-275">Hoja de referencia de SQL a Javascript</span><span class="sxs-lookup"><span data-stu-id="bb149-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="bb149-276">En la tabla siguiente se muestran varias consultas SQL con las consultas de JavaScript correspondientes.</span><span class="sxs-lookup"><span data-stu-id="bb149-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="bb149-277">Como sucede con las consultas SQL, las claves de propiedad del documento (por ejemplo, `doc.id`) distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bb149-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="bb149-278">SQL</span><span class="sxs-lookup"><span data-stu-id="bb149-278">SQL</span></span>| <span data-ttu-id="bb149-279">API de consulta de JavaScript</span><span class="sxs-lookup"><span data-stu-id="bb149-279">JavaScript Query API</span></span>|<span data-ttu-id="bb149-280">Descripción siguiente</span><span class="sxs-lookup"><span data-stu-id="bb149-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="bb149-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="bb149-281">SELECT *</span></span><br><span data-ttu-id="bb149-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="bb149-282">FROM docs</span></span>| <span data-ttu-id="bb149-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="bb149-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="bb149-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="bb149-285">});</span><span class="sxs-lookup"><span data-stu-id="bb149-285">});</span></span>|<span data-ttu-id="bb149-286">1</span><span class="sxs-lookup"><span data-stu-id="bb149-286">1</span></span>|
|<span data-ttu-id="bb149-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="bb149-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="bb149-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="bb149-288">FROM docs</span></span>|<span data-ttu-id="bb149-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-289">__.map(function(doc) {</span></span><br><span data-ttu-id="bb149-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="bb149-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="bb149-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="bb149-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="bb149-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="bb149-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="bb149-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="bb149-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="bb149-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="bb149-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="bb149-295">});</span><span class="sxs-lookup"><span data-stu-id="bb149-295">});</span></span>|<span data-ttu-id="bb149-296">2</span><span class="sxs-lookup"><span data-stu-id="bb149-296">2</span></span>|
|<span data-ttu-id="bb149-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="bb149-297">SELECT *</span></span><br><span data-ttu-id="bb149-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="bb149-298">FROM docs</span></span><br><span data-ttu-id="bb149-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="bb149-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="bb149-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="bb149-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="bb149-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="bb149-302">});</span><span class="sxs-lookup"><span data-stu-id="bb149-302">});</span></span>|<span data-ttu-id="bb149-303">3</span><span class="sxs-lookup"><span data-stu-id="bb149-303">3</span></span>|
|<span data-ttu-id="bb149-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="bb149-304">SELECT *</span></span><br><span data-ttu-id="bb149-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="bb149-305">FROM docs</span></span><br><span data-ttu-id="bb149-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="bb149-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="bb149-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="bb149-307">__.filter(function(x) {</span></span><br><span data-ttu-id="bb149-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="bb149-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="bb149-309">});</span><span class="sxs-lookup"><span data-stu-id="bb149-309">});</span></span>|<span data-ttu-id="bb149-310">4</span><span class="sxs-lookup"><span data-stu-id="bb149-310">4</span></span>|
|<span data-ttu-id="bb149-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="bb149-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="bb149-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="bb149-312">FROM docs</span></span><br><span data-ttu-id="bb149-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="bb149-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="bb149-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="bb149-314">__.chain()</span></span><br><span data-ttu-id="bb149-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="bb149-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="bb149-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="bb149-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="bb149-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="bb149-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="bb149-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="bb149-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="bb149-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="bb149-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="bb149-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="bb149-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="bb149-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="bb149-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="bb149-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="bb149-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="bb149-324">.value();</span><span class="sxs-lookup"><span data-stu-id="bb149-324">.value();</span></span>|<span data-ttu-id="bb149-325">5</span><span class="sxs-lookup"><span data-stu-id="bb149-325">5</span></span>|
|<span data-ttu-id="bb149-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="bb149-326">SELECT VALUE tag</span></span><br><span data-ttu-id="bb149-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="bb149-327">FROM docs</span></span><br><span data-ttu-id="bb149-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="bb149-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="bb149-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="bb149-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="bb149-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="bb149-330">__.chain()</span></span><br><span data-ttu-id="bb149-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="bb149-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="bb149-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="bb149-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="bb149-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="bb149-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="bb149-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="bb149-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="bb149-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="bb149-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="bb149-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="bb149-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="bb149-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="bb149-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="bb149-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="bb149-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="bb149-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="bb149-340">6</span><span class="sxs-lookup"><span data-stu-id="bb149-340">6</span></span>|

<span data-ttu-id="bb149-341">En las descripciones siguientes se explican las consultas de la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="bb149-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="bb149-342">Devuelve resultados de todos los documentos (paginados con el token de continuación) tal y como están.</span><span class="sxs-lookup"><span data-stu-id="bb149-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="bb149-343">Proyecta el id., el mensaje (con el alias msg) y la acción de todos los documentos.</span><span class="sxs-lookup"><span data-stu-id="bb149-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="bb149-344">Realiza consultas de los documentos con el predicado: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="bb149-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="bb149-345">Realiza consultas de los documentos que tengan una propiedad Tags que sea una matriz que contiene el valor 123.</span><span class="sxs-lookup"><span data-stu-id="bb149-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="bb149-346">Realiza consultas de los documentos con un predicado, id = "X998_Y998", y, después, proyecta el id. y el mensaje (con el alias msg).</span><span class="sxs-lookup"><span data-stu-id="bb149-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="bb149-347">Filtra los documentos que tienen una propiedad de matriz, Tags, y ordena los documentos resultantes por la propiedad del sistema _ts timestamp; después, proyecta + flattens en la matriz Tags.</span><span class="sxs-lookup"><span data-stu-id="bb149-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="bb149-348">Compatibilidad con el tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="bb149-348">Runtime support</span></span>
<span data-ttu-id="bb149-349">La [API del lado servidor de JavaScript de DocumentDB](http://azure.github.io/azure-documentdb-js-server/) ofrece compatibilidad con la mayoría de las características del lenguaje JavaScript habituales, según el estándar [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="bb149-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="bb149-350">Seguridad</span><span class="sxs-lookup"><span data-stu-id="bb149-350">Security</span></span>
<span data-ttu-id="bb149-351">Los procedimientos almacenados y desencadenadores de JavaScript se encuentran en un espacio aislado para que los efectos de un script no se filtren al otro sin pasar por el aislamiento de la transacción de instantánea en el nivel de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="bb149-352">Los entornos de tiempo de ejecución se agrupan pero se borran del contexto tras cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="bb149-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="bb149-353">Por lo tanto se garantiza su seguridad de cualquier efecto secundario no intencionado entre ellos.</span><span class="sxs-lookup"><span data-stu-id="bb149-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="bb149-354">Precompilación</span><span class="sxs-lookup"><span data-stu-id="bb149-354">Pre-compilation</span></span>
<span data-ttu-id="bb149-355">Los procedimientos almacenados, desencadenadores y UDF se precompilan implícitamente en formato de código byte para evitar los costes de compilación en el momento de cada invocación de script.</span><span class="sxs-lookup"><span data-stu-id="bb149-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="bb149-356">Esto garantiza que las invocaciones de los procedimientos almacenados son rápidos y tienen poca superficie.</span><span class="sxs-lookup"><span data-stu-id="bb149-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="bb149-357">Compatibilidad con SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="bb149-357">Client SDK support</span></span>
<span data-ttu-id="bb149-358">Además de la API de DocumentDB para el cliente de [Node.js](documentdb-sdk-node.md), Azure Cosmos DB tiene SDK de [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/) y [Python](documentdb-sdk-python.md) para la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bb149-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="bb149-359">Los procedimientos almacenados, desencadenadores y UDF también se pueden crear y ejecutar mediante cualquiera de estos SDK.</span><span class="sxs-lookup"><span data-stu-id="bb149-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="bb149-360">En el siguiente ejemplo se muestra cómo crear y ejecutar un procedimiento almacenado mediante el cliente.NET.</span><span class="sxs-lookup"><span data-stu-id="bb149-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="bb149-361">Observe cómo los tipos de .NET se pasan al procedimiento almacenado como JSON y se vuelven a leer.</span><span class="sxs-lookup"><span data-stu-id="bb149-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="bb149-362">En este ejemplo se muestra cómo usar la [API de .NET para DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) para crear un desencadenador previo y generar un documento con el desencadenador habilitado.</span><span class="sxs-lookup"><span data-stu-id="bb149-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="bb149-363">Y en el siguiente ejemplo se muestra cómo crear una función definida por el usuario para usarla en una [consulta de SQL de la API de DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="bb149-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="bb149-364">API de REST</span><span class="sxs-lookup"><span data-stu-id="bb149-364">REST API</span></span>
<span data-ttu-id="bb149-365">Todas las operaciones de Azure Cosmos DB se pueden realizar mediante RESTful.</span><span class="sxs-lookup"><span data-stu-id="bb149-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="bb149-366">Los procedimientos almacenados, desencadenadores y funciones definidas por el usuario se pueden registrar en una colección mediante POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb149-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="bb149-367">El siguiente es un ejemplo de cómo registrar un procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="bb149-367">The following is an example of how to register a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="bb149-368">El procedimiento almacenado se registra ejecutando una solicitud POST con el URI dbs/testdb/colls/testColl/sprocs conteniendo en el cuerpo el procedimiento almacenado que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="bb149-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="bb149-369">Los desencadenadores y las UDF se pueden registrar de forma similar mediante la emisión de una solicitud POST con respecto a /triggers y /udfs, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bb149-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="bb149-370">Este procedimiento almacenado se puede ejecutar mediante la emisión de una solicitud POST en su vínculo de recursos:</span><span class="sxs-lookup"><span data-stu-id="bb149-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="bb149-371">Aquí, la entrada del procedimiento almacenado se pasa al cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="bb149-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="bb149-372">Tenga en cuenta que la entrada se pasa como una matriz JSON de parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb149-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="bb149-373">El procedimiento almacenado toma la primera entrada como un documento que es un cuerpo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="bb149-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="bb149-374">La respuesta que recibimos es como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb149-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="bb149-375">Los desencadenadores, a diferencia de los procedimientos almacenados, no se pueden ejecutar directamente.</span><span class="sxs-lookup"><span data-stu-id="bb149-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="bb149-376">En su lugar, se ejecutan como parte de una operación en un documento.</span><span class="sxs-lookup"><span data-stu-id="bb149-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="bb149-377">Podemos especificar los desencadenadores que se van a ejecutar con una solicitud mediante los encabezados de HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb149-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="bb149-378">La siguiente es una solicitud para crear un documento.</span><span class="sxs-lookup"><span data-stu-id="bb149-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="bb149-379">Aquí el desencadenador previo que se debe ejecutar con la solicitud se especifica en el encabezado x-ms-documentdb-pre-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="bb149-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="bb149-380">Del mismo modo, cualquier desencadenador posterior se da en el encabezado x-ms-documentdb-post-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="bb149-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="bb149-381">Tenga en cuenta que tanto los desencadenadores previos como los posteriores se pueden especificar para una solicitud determinada.</span><span class="sxs-lookup"><span data-stu-id="bb149-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="bb149-382">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb149-382">Sample code</span></span>
<span data-ttu-id="bb149-383">Puede encontrar más ejemplos de código del lado servidor (entre los que se incluyen [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) y [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) en nuestro [repositorio de GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="bb149-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="bb149-384">¿Desea compartir el impresionante procedimiento almacenado?</span><span class="sxs-lookup"><span data-stu-id="bb149-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="bb149-385">Envíenos una solicitud de extracción.</span><span class="sxs-lookup"><span data-stu-id="bb149-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb149-386">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb149-386">Next steps</span></span>
<span data-ttu-id="bb149-387">Una vez que haya almacenado uno o varios procedimientos, y creado desencadenadores y funciones definidas por el usuario, puede cargarlos y verlos en Azure Portal mediante el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="bb149-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="bb149-388">También puede encontrar útiles las siguientes referencias y recursos en su camino hacia el aprendizaje de la programación del servidor de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="bb149-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="bb149-389">SDK de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bb149-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="bb149-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="bb149-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="bb149-391">JSON</span><span class="sxs-lookup"><span data-stu-id="bb149-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="bb149-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="bb149-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="bb149-393">Extensibilidad de la base de datos segura y portátil</span><span class="sxs-lookup"><span data-stu-id="bb149-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="bb149-394">Arquitectura de base de datos orientada a servicios</span><span class="sxs-lookup"><span data-stu-id="bb149-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="bb149-395">Hospedaje de runtime de .NET en Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="bb149-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

