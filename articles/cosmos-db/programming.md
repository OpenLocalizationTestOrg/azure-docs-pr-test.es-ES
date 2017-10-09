---
title: "programación de JavaScript en el aaaServer para la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse base de datos de Azure Cosmos toowrite procedimientos almacenados, desencadenadores de base de datos y funciones definidas por el usuario (UDF) en JavaScript. Obtenga sugerencias de programación de base de datos y mucho más."
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
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="24923-105">Programación en el servidor de Azure Cosmos DB: procedimientos almacenados, desencadenadores de base de datos y funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="24923-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="24923-106">Conozca cómo la ejecución transaccional integrada del lenguaje de Azure Cosmos DB de JavaScript permite a los desarrolladores escribir **procedimientos almacenados**, **desencadenadores** y **funciones definidas por el usuario (UDF)** de forma nativa en un elemento de JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/).</span><span class="sxs-lookup"><span data-stu-id="24923-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="24923-107">Esto le permite toowrite lógica de aplicación de programa de base de datos que puede distribuir y ejecutarse directamente en las particiones de almacenamiento de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="24923-108">Le recomendamos que obtenga iniciada por ver Hola después de vídeo, donde Andrew Liu proporciona un tooCosmos breve introducción de la base de datos modelo de programación de base de datos de servidor.</span><span class="sxs-lookup"><span data-stu-id="24923-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="24923-109">A continuación, devolver artículo toothis, donde obtendrá información sobre Hola respuestas toohello siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="24923-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="24923-110">¿Cómo se escribe un procedimiento almacenado, un desencadenador o una UDF con JavaScript?</span><span class="sxs-lookup"><span data-stu-id="24923-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="24923-111">¿Qué garantías ACID ofrece Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="24923-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="24923-112">¿Cómo funcionan las transacciones en Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="24923-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="24923-113">¿Qué son los desencadenadores previos y posteriores y cómo se escriben?</span><span class="sxs-lookup"><span data-stu-id="24923-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="24923-114">¿Cómo se registran y se ejecutan un procedimiento almacenado, un desencadenador o una UDF de forma compatible con REST mediante HTTP?</span><span class="sxs-lookup"><span data-stu-id="24923-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="24923-115">¿Las Cosmos DB SDK toocreate disponible y ejecutar procedimientos almacenados, desencadenadores y UDF?</span><span class="sxs-lookup"><span data-stu-id="24923-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="24923-116">Introducción tooStored procedimiento y la programación de UDF</span><span class="sxs-lookup"><span data-stu-id="24923-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="24923-117">Este enfoque de *"JavaScript como un día moderno T-SQL"* evita que los desarrolladores de aplicaciones de las complejidades de Hola de discordancias del sistema y las tecnologías de asignación objeto-relacional.</span><span class="sxs-lookup"><span data-stu-id="24923-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="24923-118">También tiene una serie de ventajas intrínsecas que pueden ser utilizados toobuild completas aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="24923-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="24923-119">**Lógica de procedimientos:** JavaScript como un lenguaje de programación de alto nivel, proporciona una interfaz enriquecida y familiar tooexpress lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="24923-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="24923-120">Puede realizar complejas secuencias de datos de toohello más cerca de las operaciones.</span><span class="sxs-lookup"><span data-stu-id="24923-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="24923-121">**Transacciones atómicas:** Cosmos DB garantiza que las operaciones de base de datos realizadas dentro de un único procedimiento almacenado o desencadenador sean atómicas.</span><span class="sxs-lookup"><span data-stu-id="24923-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="24923-122">Esto permite a una aplicación combinar operaciones relacionadas en un único lote para que todas se realicen correctamente o no lo haga ninguna.</span><span class="sxs-lookup"><span data-stu-id="24923-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="24923-123">**Rendimiento:** hecho de Hola que JSON es intrínsecamente asignadas toohello Javascript language type system y es también la unidad básica de Hola de almacenamiento en la base de datos de Cosmos permite un número de optimizaciones como diferida materialización de JSON se documenta en el búfer de Hola grupo y dejándolos disponible toohello petición ejecutar código.</span><span class="sxs-lookup"><span data-stu-id="24923-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="24923-124">Hay más ventajas de rendimiento asociados a la base de datos toohello lógica de negocios trasvase:</span><span class="sxs-lookup"><span data-stu-id="24923-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="24923-125">Procesamiento por lotes: los desarrolladores pueden agrupar operaciones como inserciones y enviarlas en masa.</span><span class="sxs-lookup"><span data-stu-id="24923-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="24923-126">costo de latencia de tráfico de red de Hola y transacciones independientes de hello almacén toocreate sobrecarga se reducción significativamente.</span><span class="sxs-lookup"><span data-stu-id="24923-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="24923-127">Precompilación: Cosmos DB precompila procedimientos almacenados, desencadenadores y definidos por el usuario (UDF) funciones tooavoid costo de compilación de JavaScript para cada invocación.</span><span class="sxs-lookup"><span data-stu-id="24923-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="24923-128">Hello sobrecarga de la generación de código de bytes de hello para la lógica de procedimientos de hello es había amortizado tooa un valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="24923-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="24923-129">Secuenciación: muchas operaciones necesitan un efecto secundario (“desencadenador”) que implica potencialmente realizar una o más operaciones de almacenamiento secundarias.</span><span class="sxs-lookup"><span data-stu-id="24923-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="24923-130">Además de atomicidad, esto tiene un mejor rendimiento al mover servidor toohello.</span><span class="sxs-lookup"><span data-stu-id="24923-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="24923-131">**Encapsulación:** procedimientos almacenados pueden ser utilizados toogroup lógica de negocios en un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="24923-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="24923-132">Esto tiene dos ventajas:</span><span class="sxs-lookup"><span data-stu-id="24923-132">This has two advantages:</span></span>
  * <span data-ttu-id="24923-133">Agrega una capa de abstracción sobre los datos sin procesar de hello, que permite que sus aplicaciones independientemente de los datos de hello tooevolve arquitectos de datos.</span><span class="sxs-lookup"><span data-stu-id="24923-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="24923-134">Esto es especialmente ventajoso cuando Hola datos sin esquema debido toohello suposiciones complicado que necesitan toobe incrustada en la aplicación hello si tienen toodeal con datos directamente.</span><span class="sxs-lookup"><span data-stu-id="24923-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="24923-135">Esta abstracción permite a las empresas proteger sus datos mediante la optimización de acceso de Hola desde scripts de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="24923-136">Hello creación y ejecución de desencadenadores de base de datos, procedimiento almacenado y operadores de consulta personalizada se admite a través de hello [API de REST](/rest/api/documentdb/), [estudio de DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases), y [SDKdecliente](documentdb-sdk-dotnet.md) en numerosas plataformas incluidas. NET, Node.js y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="24923-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="24923-137">Este tutorial usa hello [SDK de Node.js con preguntas promesas](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sintaxis y el uso de procedimientos almacenados, desencadenadores y UDF.</span><span class="sxs-lookup"><span data-stu-id="24923-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="24923-138">Procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="24923-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="24923-139">Ejemplo: creación de un procedimiento almacenado sencillo</span><span class="sxs-lookup"><span data-stu-id="24923-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="24923-140">Comencemos con un sencillo procedimiento almacenado que devuelve una respuesta “Hello World”.</span><span class="sxs-lookup"><span data-stu-id="24923-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="24923-141">Los procedimientos almacenados se registran por colección y pueden funcionar en cualquier documento y dato adjunto presente en esa colección.</span><span class="sxs-lookup"><span data-stu-id="24923-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="24923-142">Hello fragmento de código siguiente muestra cómo tooregister Hola helloWorld procedimiento almacenado con una colección.</span><span class="sxs-lookup"><span data-stu-id="24923-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="24923-143">Una vez que se registra el procedimiento almacenado de hello, podemos ejecutar con la colección de Hola y leer los resultados de hello en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="24923-144">objeto de contexto de Hello proporciona acceso tooall operaciones que pueden realizarse en el almacenamiento de base de datos de Cosmos, así como tener acceso a los objetos de solicitud y respuesta de toohello.</span><span class="sxs-lookup"><span data-stu-id="24923-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="24923-145">En este caso, hemos usado Hola respuesta tooset Hola el cuerpo del objeto de respuesta de Hola que envió el cliente toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="24923-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="24923-146">Para obtener más información, consulte toohello [server documentación del SDK de Azure Cosmos DB JavaScript](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="24923-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="24923-147">Permítanos ampliar este ejemplo y agregar más funciones relacionadas con la base de datos toohello de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="24923-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="24923-148">Los procedimientos almacenados pueden crear, actualizar, leer, consultar y eliminar los documentos y datos adjuntos dentro de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="24923-149">Ejemplo: Escribir un procedimiento almacenado toocreate un documento</span><span class="sxs-lookup"><span data-stu-id="24923-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="24923-150">el fragmento siguiente de Hello muestra cómo toouse Hola toointeract del objeto de contexto con recursos de base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="24923-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

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


<span data-ttu-id="24923-151">Este procedimiento almacenado toma como entrada documentToCreate, cuerpo de Hola de un toobe documento creado en la colección actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="24923-152">Todas estas operaciones son asíncronas y dependen de las devoluciones de llamadas de función de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="24923-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="24923-153">función de devolución de llamada de Hello tiene dos parámetros, uno para el objeto de error de hello en caso de que se produce un error en la operación de Hola y uno para hello creó el objeto.</span><span class="sxs-lookup"><span data-stu-id="24923-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="24923-154">Dentro de la devolución de llamada de hello, los usuarios pueden controlar la excepción de Hola o producir un error.</span><span class="sxs-lookup"><span data-stu-id="24923-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="24923-155">En caso de que no se proporciona una devolución de llamada y se produce un error, el tiempo de ejecución de base de datos de Azure Cosmos Hola produce un error.</span><span class="sxs-lookup"><span data-stu-id="24923-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="24923-156">En el ejemplo de Hola anterior, devolución de llamada de hello produce un error si el error en la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="24923-157">En caso contrario, Establece Id. de Hola de hello creado el documento como cuerpo del mensaje del cliente de toohello de respuesta de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="24923-158">A continuación se explica cómo se ejecuta este procedimiento almacenado con parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="24923-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
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


<span data-ttu-id="24923-159">Tenga en cuenta que este procedimiento almacenado puede ser modificado tootake una matriz de los cuerpos de documento como entrada y crearlos en hello mismo almacenado ejecución del procedimiento en lugar de la red varias solicitudes toocreate de ellos individualmente.</span><span class="sxs-lookup"><span data-stu-id="24923-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="24923-160">Esto puede ser usado tooimplement un importador masiva eficaz para la base de datos de Cosmos (se explica más adelante en este tutorial).</span><span class="sxs-lookup"><span data-stu-id="24923-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="24923-161">ejemplo de Hola descrito muestra cómo procedimientos almacenados del toouse.</span><span class="sxs-lookup"><span data-stu-id="24923-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="24923-162">Desencadenadores y funciones definidas por el usuario (UDF) se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="24923-163">Transacciones del programa de base de datos</span><span class="sxs-lookup"><span data-stu-id="24923-163">Database program transactions</span></span>
<span data-ttu-id="24923-164">Una transacción en una base de datos típica se puede definir como una secuencia de operaciones realizadas como una única unidad lógica de trabajo.</span><span class="sxs-lookup"><span data-stu-id="24923-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="24923-165">Cada transacción proporciona **garantías ACID**.</span><span class="sxs-lookup"><span data-stu-id="24923-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="24923-166">ACID es un acrónimo conocido que, por sus siglas en inglés, hace referencia a cuatro propiedades: Atomicidad, Coherencia, Aislamiento y Durabilidad.</span><span class="sxs-lookup"><span data-stu-id="24923-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="24923-167">En pocas palabras, la atomicidad garantiza que todo el trabajo Hola realizado dentro de una transacción se trata como una sola unidad donde cualquier toda ella se confirma o ninguno.</span><span class="sxs-lookup"><span data-stu-id="24923-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="24923-168">Coherencia se asegura de que los datos de hello siempre están en buen estado interno a través de las transacciones.</span><span class="sxs-lookup"><span data-stu-id="24923-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="24923-169">Aislamiento garantiza que no haya dos transacciones interfieren entre sí: por lo general, más comerciales sistemas proporcionan varios niveles de aislamiento que se pueden usar en función de las necesidades de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="24923-170">Durabilidad se garantiza que cualquier cambio que se confirma en la base de datos de hello siempre estará presente.</span><span class="sxs-lookup"><span data-stu-id="24923-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="24923-171">En la base de datos de Cosmos, JavaScript se hospeda en hello mismo espacio de memoria como base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="24923-172">Por lo tanto, las solicitudes realizadas dentro de procedimientos almacenados y desencadenadores ejecutan en hello mismo ámbito de una sesión de base de datos.</span><span class="sxs-lookup"><span data-stu-id="24923-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="24923-173">Esto permite Cosmos DB tooguarantee ACID para todas las operaciones que forman parte de un único procedimiento almacenado o desencadenador.</span><span class="sxs-lookup"><span data-stu-id="24923-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="24923-174">Tenga en cuenta los siguiente Hola almacena la definición del procedimiento:</span><span class="sxs-lookup"><span data-stu-id="24923-174">Consider hello following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="24923-175">Este procedimiento almacenado usa transacciones en un juego aplicación tootrade de los elementos entre dos jugadores en una sola operación.</span><span class="sxs-lookup"><span data-stu-id="24923-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="24923-176">Hola almacenado cada jugador toohello correspondiente identificadores pasa como un argumento de procedimiento intentos tooread dos documentos.</span><span class="sxs-lookup"><span data-stu-id="24923-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="24923-177">Si se encuentran ambos documentos Reproductor, procedimiento almacenado de hello actualiza documentos Hola intercambiando sus elementos.</span><span class="sxs-lookup"><span data-stu-id="24923-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="24923-178">Si se detectan errores durante el proceso de hello, produce una excepción de JavaScript que implícitamente anula la transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="24923-179">Si hello procedimiento Hola almacenado de recopilación se ha registrado con es una colección única partición, entonces transacción hello es tooall ámbito Hola documentos dentro de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="24923-180">Si la colección de hello tiene particiones, los procedimientos almacenados se ejecutan en el ámbito de transacción de Hola de una clave de partición única.</span><span class="sxs-lookup"><span data-stu-id="24923-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="24923-181">Cada uno de ellos almacenados de ejecución del procedimiento, a continuación, debe incluir un valor de clave de partición debe ejecutarse toohello ámbito hello de la transacción correspondiente en.</span><span class="sxs-lookup"><span data-stu-id="24923-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="24923-182">Para más información, consulte [Creación de particiones con Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="24923-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="24923-183">Confirmación y reversión</span><span class="sxs-lookup"><span data-stu-id="24923-183">Commit and rollback</span></span>
<span data-ttu-id="24923-184">Las transacciones están integradas de forma profunda y nativa en el modelo de programación de JavaScript de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="24923-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="24923-185">Dentro de una función de JavaScript, todas las operaciones se ajustan automáticamente en una única transacción.</span><span class="sxs-lookup"><span data-stu-id="24923-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="24923-186">Si hello JavaScript finalice sin ninguna excepción, base de datos de hello operations toohello se confirman.</span><span class="sxs-lookup"><span data-stu-id="24923-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="24923-187">En efecto, las instrucciones de "BEGIN TRANSACTION" y "COMMIT TRANSACTION" hello en bases de datos relacionales están implícitas en base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="24923-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="24923-188">Si se produce cualquier excepción que se propaga desde el script de Hola, tiempo de ejecución de JavaScript de Cosmos DB revertirá toda transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="24923-189">Como se muestra en hello anteriormente ejemplo, producir una excepción es realmente el equivalente tooa "ROLLBACK TRANSACTION" en la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="24923-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="24923-190">Coherencia de datos</span><span class="sxs-lookup"><span data-stu-id="24923-190">Data consistency</span></span>
<span data-ttu-id="24923-191">Desencadenadores y procedimientos almacenados se ejecutan siempre en la réplica principal de Hola de contenedor de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="24923-192">Esto garantiza que las lecturas desde dentro de los procedimientos almacenados ofrecen una fuerte coherencia.</span><span class="sxs-lookup"><span data-stu-id="24923-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="24923-193">Se pueden ejecutar consultas con funciones definidas por el usuario en Hola principal o cualquier réplica secundaria, pero asegúrese de toomeet Hola solicitado nivel de coherencia eligiendo réplica adecuado Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="24923-194">Ejecución vinculada</span><span class="sxs-lookup"><span data-stu-id="24923-194">Bounded execution</span></span>
<span data-ttu-id="24923-195">Todas las operaciones de base de datos de Cosmos deben completarse dentro de servidor hello especificado duración de tiempo de espera de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="24923-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="24923-196">Esta restricción también aplica a las funciones de tooJavaScript (procedimientos almacenados, desencadenadores y funciones definidas por el usuario).</span><span class="sxs-lookup"><span data-stu-id="24923-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="24923-197">Si no completó una operación con ese límite de tiempo, se revierten las transacciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="24923-198">Funciones de JavaScript deben finalizó dentro del límite de tiempo de Hola o implementar una continuación según modelar toobatch/reanudar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="24923-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="24923-199">En el desarrollo de toosimplify orden almacenado procedimientos y desencadenadores toohandle límites de tiempo, todas las funciones en el objeto de colección de hello (para crear, leer, reemplazar y eliminación de documentos y datos adjuntos) devuelven un valor booleano que representa si la operación se completó.</span><span class="sxs-lookup"><span data-stu-id="24923-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="24923-200">Si este valor es false, es una indicación que límite de tiempo de hello es sobre tooexpire y ese procedimiento Hola debe contener la ejecución.</span><span class="sxs-lookup"><span data-stu-id="24923-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="24923-201">Operaciones en cola toohello previa la primera operación de almacén no aceptado se garantizan toocomplete si procedimiento almacenado de hello completa en el tiempo y no en cola las solicitudes más.</span><span class="sxs-lookup"><span data-stu-id="24923-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="24923-202">Las funciones de JavaScript también se vinculan al consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="24923-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="24923-203">COSMOS DB reserva el rendimiento por la colección basándose en el tamaño de hello aprovisionado de una cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="24923-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="24923-204">La capacidad de proceso se expresa en términos de una unidad de CPU normalizada, consumo de memoria y E/S llamadas unidades de solicitud o RU.</span><span class="sxs-lookup"><span data-stu-id="24923-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="24923-205">Funciones de JavaScript potencialmente pueden utilizar un gran número de RUs en poco tiempo y podrían obtener velocidad limitado si se alcanza el límite de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="24923-206">Procedimientos almacenados de uso intensivo de recursos también pueden ser disponibilidad tooensure en cuarentena de operaciones de base de datos primitivo.</span><span class="sxs-lookup"><span data-stu-id="24923-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="24923-207">Ejemplo: importación masiva de datos a un programa de base de datos</span><span class="sxs-lookup"><span data-stu-id="24923-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="24923-208">A continuación se muestra un ejemplo de un procedimiento almacenado que se escribe toobulk importar documentos en una colección.</span><span class="sxs-lookup"><span data-stu-id="24923-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="24923-209">Tenga en cuenta cómo Hola almacena la ejecución del procedimiento identificadores limitados activando Hola booleano devolver valor de createDocument y, a continuación, utiliza Hola número de documentos que se insertan en cada invocación del procedimiento tootrack y reanudar progreso de hello almacenado en lotes.</span><span class="sxs-lookup"><span data-stu-id="24923-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="24923-210"><a id="trigger"></a> Desencadenadores de base de datos</span><span class="sxs-lookup"><span data-stu-id="24923-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="24923-211">Desencadenadores previos de base de datos</span><span class="sxs-lookup"><span data-stu-id="24923-211">Database pre-triggers</span></span>
<span data-ttu-id="24923-212">Cosmos DB proporciona desencadenadores que se ejecutan o desencadenan por una operación en un documento.</span><span class="sxs-lookup"><span data-stu-id="24923-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="24923-213">Por ejemplo, puede especificar un desencadenador anterior cuando está creando un documento: este desencadenador anterior se ejecutará antes de que se crea el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="24923-214">Hola te mostramos un ejemplo de cómo desencadenadores previos pueden ser usado toovalidate Hola propiedades de un documento que se va a crear:</span><span class="sxs-lookup"><span data-stu-id="24923-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="24923-215">Hello correspondiente código de registro del lado cliente de Node.js para un desencadenador de Hola y:</span><span class="sxs-lookup"><span data-stu-id="24923-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

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


<span data-ttu-id="24923-216">Los desencadenadores previos no pueden tener parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="24923-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="24923-217">objeto de solicitud de Hello puede ser el mensaje de solicitud de hello toomanipulate utilizados asociado a la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="24923-218">En este caso, desencadenador previo Hola se ejecuta con la creación de hello de un documento y cuerpo del mensaje de solicitud de hello contiene Hola documento toobe creado en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="24923-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="24923-219">Cuando se registren los desencadenadores, los usuarios pueden especificar operaciones de Hola que se pueden ejecutar con.</span><span class="sxs-lookup"><span data-stu-id="24923-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="24923-220">Este desencadenador se creó con TriggerOperation.Create, lo que significa que no se permite la continuación de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="24923-221">Desencadenadores anteriores de base de datos</span><span class="sxs-lookup"><span data-stu-id="24923-221">Database post-triggers</span></span>
<span data-ttu-id="24923-222">Los desencadenadores posteriores, del mismo modo que los previos, se asocian con una operación de un documento y no aceptan parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="24923-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="24923-223">Se ejecutan **después** Hola operación se ha completado y tiene el mensaje de respuesta de toohello de acceso que se envía el cliente toohello.</span><span class="sxs-lookup"><span data-stu-id="24923-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="24923-224">Hola siguiente ejemplo muestra los desencadenadores posteriores en acción:</span><span class="sxs-lookup"><span data-stu-id="24923-224">hello following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="24923-225">desencadenador de Hola se puede registrar como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
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


<span data-ttu-id="24923-226">Este desencadenador consulta documento de metadatos de Hola y actualiza con detalles sobre el documento de hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="24923-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="24923-227">Algo que es importante toonote es hello **transaccional** ejecución de desencadenadores en la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="24923-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="24923-228">Este desencadenador posterior a la que se ejecuta como parte del programa Hola misma transacción como la creación de hello del documento original de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="24923-229">Por lo tanto, si se produce una excepción del desencadenador posterior a la de hello (por ejemplo si estamos documento de metadatos de hello no se puede tooupdate), transacción entera Hola se producirá un error y se revierte.</span><span class="sxs-lookup"><span data-stu-id="24923-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="24923-230">No se creará ningún documento y se devolverá una excepción.</span><span class="sxs-lookup"><span data-stu-id="24923-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="24923-231"><a id="udf"></a>Funciones definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="24923-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="24923-232">Funciones definidas por el usuario (UDF) son la gramática del lenguaje de consulta de tooextend usado Hola documentos API SQL e implementan lógica de negocios personalizada.</span><span class="sxs-lookup"><span data-stu-id="24923-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="24923-233">Solo se las puede llamar desde consultas internas.</span><span class="sxs-lookup"><span data-stu-id="24923-233">They can only be called from inside queries.</span></span> <span data-ttu-id="24923-234">Que no tiene el objeto de contexto de acceso toohello y sirven de toobe utilizado como JavaScript solo proceso.</span><span class="sxs-lookup"><span data-stu-id="24923-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="24923-235">Por lo tanto, se pueden ejecutar UDF en las réplicas secundarias de hello servicio base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="24923-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="24923-236">Hello en el ejemplo siguiente crea un UDF toocalculate impuesto, basándose en las tasas para distintos corchetes de ingresos y, a continuación, lo usa dentro de una consulta toofind todas las personas que más de 20.000 $ de pago de impuestos.</span><span class="sxs-lookup"><span data-stu-id="24923-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="24923-237">Hola UDF puede utilizarse posteriormente en las consultas como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="24923-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="24923-238">API de consulta integradas en lenguajes JavaScript</span><span class="sxs-lookup"><span data-stu-id="24923-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="24923-239">Además tooissuing consultas con la gramática SQL de DocumentDB, hello servidor SDK permiten consultas tooperform optimizado mediante una interfaz de JavaScript fluida sin ningún conocimiento de SQL.</span><span class="sxs-lookup"><span data-stu-id="24923-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="24923-240">consulta de JavaScript de Hello que API permite tooprogrammatically compilación consultas al pasar las funciones de predicado a la función encadenable llama, con un tooECMAScript5 familiar sintaxis elementos integrados de matriz y populares bibliotecas de JavaScript como lodash.</span><span class="sxs-lookup"><span data-stu-id="24923-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="24923-241">Hola JavaScript en tiempo de ejecución toobe ejecutado eficazmente con índices de Azure Cosmos DB analiza las consultas.</span><span class="sxs-lookup"><span data-stu-id="24923-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="24923-242">`__`(doble subrayado) es un alias demasiado`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="24923-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="24923-243">En otras palabras, puede usar `__` o `getContext().getCollection()` tooaccess Hola API de consulta de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="24923-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="24923-244">Estas son algunas de las funciones compatibles:</span><span class="sxs-lookup"><span data-stu-id="24923-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="24923-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-246">Inicia una llamada encadenada que debe terminarse con value().</span><span class="sxs-lookup"><span data-stu-id="24923-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="24923-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-248">Filtra hello mediante una función de predicado que devuelve true o false en orden toofilter documentos de entrada de entrada/salida en el conjunto resultante de Hola de entrada.</span><span class="sxs-lookup"><span data-stu-id="24923-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="24923-249">Este comportamiento es similar tooa cláusula WHERE de SQL.</span><span class="sxs-lookup"><span data-stu-id="24923-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="24923-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-251">Se aplica una proyección dada una función de transformación que se asigna cada objeto de JavaScript de tooa de elemento de entrada o valor.</span><span class="sxs-lookup"><span data-stu-id="24923-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="24923-252">Este comportamiento es similar cláusula SELECT tooa en SQL.</span><span class="sxs-lookup"><span data-stu-id="24923-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="24923-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-254">Se trata de un método abreviado de un mapa que extrae el valor de Hola de una propiedad única de cada elemento de entrada.</span><span class="sxs-lookup"><span data-stu-id="24923-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="24923-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-256">Combina y reduce las matrices de cada elemento de entrada de matriz único tooa.</span><span class="sxs-lookup"><span data-stu-id="24923-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="24923-257">Este comportamiento es similar tooSelectMany en LINQ.</span><span class="sxs-lookup"><span data-stu-id="24923-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="24923-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-259">Generar un nuevo conjunto de documentos de ordenación de los documentos de hello en secuencia de documento de entrada de hello en orden ascendente mediante Hola dado el predicado.</span><span class="sxs-lookup"><span data-stu-id="24923-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="24923-260">Este comportamiento es similar tooa cláusula ORDER BY de SQL.</span><span class="sxs-lookup"><span data-stu-id="24923-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="24923-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="24923-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="24923-262">Generar un nuevo conjunto de documentos de ordenación de los documentos de hello en secuencia de documento de entrada de hello en orden descendente mediante Hola dado el predicado.</span><span class="sxs-lookup"><span data-stu-id="24923-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="24923-263">Este comportamiento es similar tooa ORDER BY x DESC cláusula de SQL.</span><span class="sxs-lookup"><span data-stu-id="24923-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="24923-264">Cuando se incluye dentro de las funciones de predicado o selector, hello siguientes construcciones de JavaScript obtener automáticamente optimizado toorun directamente en la base de datos de Azure Cosmos índices:</span><span class="sxs-lookup"><span data-stu-id="24923-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="24923-265">Operadores simples: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="24923-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="24923-266">Literales, incluidos el literal de objeto hello: {}</span><span class="sxs-lookup"><span data-stu-id="24923-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="24923-267">var, return</span><span class="sxs-lookup"><span data-stu-id="24923-267">var, return</span></span>

<span data-ttu-id="24923-268">Hola JavaScript siguiente construye no obtener optimizada para los índices de base de datos de Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="24923-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="24923-269">Control de flujo (por ejemplo: if, for, while)</span><span class="sxs-lookup"><span data-stu-id="24923-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="24923-270">Llamadas a funciones</span><span class="sxs-lookup"><span data-stu-id="24923-270">Function calls</span></span>

<span data-ttu-id="24923-271">Para obtener más información, consulte [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="24923-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="24923-272">Ejemplo: Escribir un procedimiento almacenado mediante la API de consulta de JavaScript de Hola</span><span class="sxs-lookup"><span data-stu-id="24923-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="24923-273">Hola siguiendo el ejemplo de código es un ejemplo de cómo puede usarse Hola API de consulta de JavaScript en el contexto de Hola de un procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="24923-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="24923-274">Inserta un documento, proporcionado por un parámetro de entrada, Hello procedimiento almacenado y actualiza un documento de metadatos, mediante hello `__.filter()` método con minSize, maxSize y totalSize en función de la propiedad de tamaño del documento entrada Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="24923-275">Hoja de referencia SQL tooJavascript</span><span class="sxs-lookup"><span data-stu-id="24923-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="24923-276">Hello tabla siguiente presenta varias consultas SQL y las consultas de JavaScript correspondientes Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="24923-277">Como sucede con las consultas SQL, las claves de propiedad del documento (por ejemplo, `doc.id`) distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="24923-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="24923-278">SQL</span><span class="sxs-lookup"><span data-stu-id="24923-278">SQL</span></span>| <span data-ttu-id="24923-279">API de consulta de JavaScript</span><span class="sxs-lookup"><span data-stu-id="24923-279">JavaScript Query API</span></span>|<span data-ttu-id="24923-280">Descripción siguiente</span><span class="sxs-lookup"><span data-stu-id="24923-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="24923-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="24923-281">SELECT *</span></span><br><span data-ttu-id="24923-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="24923-282">FROM docs</span></span>| <span data-ttu-id="24923-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="24923-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="24923-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="24923-285">});</span><span class="sxs-lookup"><span data-stu-id="24923-285">});</span></span>|<span data-ttu-id="24923-286">1</span><span class="sxs-lookup"><span data-stu-id="24923-286">1</span></span>|
|<span data-ttu-id="24923-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="24923-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="24923-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="24923-288">FROM docs</span></span>|<span data-ttu-id="24923-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-289">__.map(function(doc) {</span></span><br><span data-ttu-id="24923-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="24923-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="24923-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="24923-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="24923-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="24923-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="24923-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="24923-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="24923-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="24923-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="24923-295">});</span><span class="sxs-lookup"><span data-stu-id="24923-295">});</span></span>|<span data-ttu-id="24923-296">2</span><span class="sxs-lookup"><span data-stu-id="24923-296">2</span></span>|
|<span data-ttu-id="24923-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="24923-297">SELECT *</span></span><br><span data-ttu-id="24923-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="24923-298">FROM docs</span></span><br><span data-ttu-id="24923-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="24923-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="24923-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="24923-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="24923-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="24923-302">});</span><span class="sxs-lookup"><span data-stu-id="24923-302">});</span></span>|<span data-ttu-id="24923-303">3</span><span class="sxs-lookup"><span data-stu-id="24923-303">3</span></span>|
|<span data-ttu-id="24923-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="24923-304">SELECT *</span></span><br><span data-ttu-id="24923-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="24923-305">FROM docs</span></span><br><span data-ttu-id="24923-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="24923-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="24923-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="24923-307">__.filter(function(x) {</span></span><br><span data-ttu-id="24923-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags &amp;&amp; x.Tags.indexOf(123) &gt; -1;</span><span class="sxs-lookup"><span data-stu-id="24923-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="24923-309">});</span><span class="sxs-lookup"><span data-stu-id="24923-309">});</span></span>|<span data-ttu-id="24923-310">4</span><span class="sxs-lookup"><span data-stu-id="24923-310">4</span></span>|
|<span data-ttu-id="24923-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="24923-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="24923-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="24923-312">FROM docs</span></span><br><span data-ttu-id="24923-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="24923-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="24923-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="24923-314">__.chain()</span></span><br><span data-ttu-id="24923-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="24923-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="24923-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="24923-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="24923-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="24923-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="24923-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="24923-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="24923-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="24923-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="24923-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="24923-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="24923-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;};</span><span class="sxs-lookup"><span data-stu-id="24923-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="24923-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="24923-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="24923-324">.value();</span><span class="sxs-lookup"><span data-stu-id="24923-324">.value();</span></span>|<span data-ttu-id="24923-325">5</span><span class="sxs-lookup"><span data-stu-id="24923-325">5</span></span>|
|<span data-ttu-id="24923-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="24923-326">SELECT VALUE tag</span></span><br><span data-ttu-id="24923-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="24923-327">FROM docs</span></span><br><span data-ttu-id="24923-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="24923-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="24923-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="24923-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="24923-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="24923-330">__.chain()</span></span><br><span data-ttu-id="24923-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="24923-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.Tags &amp;&amp; Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="24923-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="24923-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="24923-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="24923-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="24923-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="24923-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="24923-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="24923-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="24923-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="24923-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="24923-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="24923-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="24923-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="24923-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="24923-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="24923-340">6</span><span class="sxs-lookup"><span data-stu-id="24923-340">6</span></span>|

<span data-ttu-id="24923-341">Hello las descripciones siguientes explican cada consulta en la tabla de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="24923-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="24923-342">Devuelve resultados de todos los documentos (paginados con el token de continuación) tal y como están.</span><span class="sxs-lookup"><span data-stu-id="24923-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="24923-343">Id. de Hola de proyectos, mensaje (alias toomsg) y acción de todos los documentos.</span><span class="sxs-lookup"><span data-stu-id="24923-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="24923-344">Las consultas para los documentos con predicado hello: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="24923-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="24923-345">Las consultas para los documentos que tengan una propiedad de etiquetas y etiquetas es una matriz que contiene el valor de hello 123.</span><span class="sxs-lookup"><span data-stu-id="24923-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="24923-346">Las consultas para los documentos con un predicado, id = "X998_Y998" y, a continuación, Id. de Hola de proyectos y mensajes (con alias toomsg).</span><span class="sxs-lookup"><span data-stu-id="24923-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="24923-347">Filtra los documentos que tienen una propiedad de matriz, etiquetas, y ordena los documentos resultantes Hola por propiedad del sistema de hello _ts marca de tiempo y a continuación, proyecta + aplana la matriz de etiquetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="24923-348">Compatibilidad con el tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="24923-348">Runtime support</span></span>
<span data-ttu-id="24923-349">[API de lado de servidor de DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) Hola proporciona compatibilidad con la mayoría de hello principales características del lenguaje JavaScript como normalizado por [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="24923-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="24923-350">Seguridad</span><span class="sxs-lookup"><span data-stu-id="24923-350">Security</span></span>
<span data-ttu-id="24923-351">JavaScript procedimientos almacenados y desencadenadores son en recintos de seguridad para que los efectos de Hola de una secuencia de comandos no pierden toohello otro sin tener que pasar a través de aislamiento de transacción de instantánea de hello en el nivel de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="24923-352">entornos de tiempo de ejecución de Hello están agrupados pero se limpian del contexto de hello después de cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="24923-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="24923-353">Por lo tanto, garantiza que sean toobe seguro para la ejecución de los efectos secundarios imprevistos entre sí.</span><span class="sxs-lookup"><span data-stu-id="24923-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="24923-354">Precompilación</span><span class="sxs-lookup"><span data-stu-id="24923-354">Pre-compilation</span></span>
<span data-ttu-id="24923-355">Los procedimientos almacenados, desencadenadores y UDF son implícitamente precompilado toohello formato de código de bytes en el costo de compilación de orden tooavoid en tiempo de Hola de cada invocación del script.</span><span class="sxs-lookup"><span data-stu-id="24923-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="24923-356">Esto garantiza que las invocaciones de los procedimientos almacenados son rápidos y tienen poca superficie.</span><span class="sxs-lookup"><span data-stu-id="24923-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="24923-357">Compatibilidad con SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="24923-357">Client SDK support</span></span>
<span data-ttu-id="24923-358">En suma toohello API de documentos para [Node.js](documentdb-sdk-node.md) cliente, base de datos de Azure Cosmos tiene [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), y [SDK de Python](documentdb-sdk-python.md) para hello API de documentos.</span><span class="sxs-lookup"><span data-stu-id="24923-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="24923-359">Los procedimientos almacenados, desencadenadores y UDF también se pueden crear y ejecutar mediante cualquiera de estos SDK.</span><span class="sxs-lookup"><span data-stu-id="24923-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="24923-360">Hola siguiente ejemplo se muestra cómo toocreate y ejecutar un procedimiento almacenado mediante el cliente de .NET de Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="24923-361">Tenga en cuenta cómo se pasan los tipos de .NET de hello en hello procedimiento almacenado como JSON y lea el contenido.</span><span class="sxs-lookup"><span data-stu-id="24923-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="24923-362">Este ejemplo se muestra cómo hello toouse [API de .NET de DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate un desencadenador anterior y crear un documento con desencadenador Hola habilitado.</span><span class="sxs-lookup"><span data-stu-id="24923-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

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


<span data-ttu-id="24923-363">Y Hola de ejemplo siguiente muestra cómo define las toocreate un usuario (UDF) de la función y usarlo en un [consulta documentos API SQL](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="24923-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="24923-364">API de REST</span><span class="sxs-lookup"><span data-stu-id="24923-364">REST API</span></span>
<span data-ttu-id="24923-365">Todas las operaciones de Azure Cosmos DB se pueden realizar mediante RESTful.</span><span class="sxs-lookup"><span data-stu-id="24923-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="24923-366">Los procedimientos almacenados, desencadenadores y funciones definidas por el usuario se pueden registrar en una colección mediante POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="24923-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="24923-367">Hello aquí te mostramos un ejemplo de cómo tooregister un procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="24923-367">hello following is an example of how tooregister a stored procedure:</span></span>

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


<span data-ttu-id="24923-368">Hello procedimiento almacenado se ha registrado mediante la ejecución de una solicitud POST contra Hola URI bases de datos/testdb/colls/testColl/sprocs Hola cuerpo que contenga Hola toocreate de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="24923-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="24923-369">Los desencadenadores y las UDF se pueden registrar de forma similar mediante la emisión de una solicitud POST con respecto a /triggers y /udfs, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="24923-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="24923-370">Este procedimiento almacenado se puede ejecutar mediante la emisión de una solicitud POST en su vínculo de recursos:</span><span class="sxs-lookup"><span data-stu-id="24923-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="24923-371">En este caso, se pasa al procedimiento toohello entrada almacenado Hola Hola del cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="24923-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="24923-372">Tenga en cuenta que la entrada de Hola se pasa como una matriz JSON de parámetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="24923-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="24923-373">Hola almacena la primera entrada de procedimiento toma Hola como un documento que forma un cuerpo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="24923-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="24923-374">respuesta de Hola que recibimos es como sigue:</span><span class="sxs-lookup"><span data-stu-id="24923-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="24923-375">Los desencadenadores, a diferencia de los procedimientos almacenados, no se pueden ejecutar directamente.</span><span class="sxs-lookup"><span data-stu-id="24923-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="24923-376">En su lugar, se ejecutan como parte de una operación en un documento.</span><span class="sxs-lookup"><span data-stu-id="24923-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="24923-377">Podemos especificar Hola desencadenadores toorun con una solicitud mediante encabezados HTTP.</span><span class="sxs-lookup"><span data-stu-id="24923-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="24923-378">Hola aquí te mostramos toocreate un documento de solicitud.</span><span class="sxs-lookup"><span data-stu-id="24923-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="24923-379">Aquí se especifica Hola desencadenador previo toobe ejecutar con la solicitud de hello en encabezado x-ms-documentdb-pre-trigger-include Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="24923-380">En consecuencia, los desencadenadores posteriores se proporcionan en encabezado x-ms-documentdb-post-trigger-include Hola.</span><span class="sxs-lookup"><span data-stu-id="24923-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="24923-381">Tenga en cuenta que tanto los desencadenadores previos como los posteriores se pueden especificar para una solicitud determinada.</span><span class="sxs-lookup"><span data-stu-id="24923-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="24923-382">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="24923-382">Sample code</span></span>
<span data-ttu-id="24923-383">Puede encontrar más ejemplos de código del lado servidor (entre los que se incluyen [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) y [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) en nuestro [repositorio de GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="24923-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="24923-384">¿Desea que el procedimiento almacenado Maravilla tooshare?</span><span class="sxs-lookup"><span data-stu-id="24923-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="24923-385">Envíenos una solicitud de extracción.</span><span class="sxs-lookup"><span data-stu-id="24923-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="24923-386">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24923-386">Next steps</span></span>
<span data-ttu-id="24923-387">Una vez que tenga uno o más procedimientos almacenados, desencadenadores y funciones definidas por el usuario creadas, puede cargarlos y verlos en hello portal de Azure mediante el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="24923-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="24923-388">También puede buscar siguiente Hola referencias y recursos útiles para su toolearn de ruta de acceso más información acerca de la programación del servidor de base de datos de Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="24923-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="24923-389">SDK de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="24923-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="24923-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="24923-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="24923-391">JSON</span><span class="sxs-lookup"><span data-stu-id="24923-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="24923-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="24923-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="24923-393">Extensibilidad de la base de datos segura y portátil</span><span class="sxs-lookup"><span data-stu-id="24923-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="24923-394">Arquitectura de base de datos orientada a servicios</span><span class="sxs-lookup"><span data-stu-id="24923-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="24923-395">Hola de hospedaje en tiempo de ejecución de .NET en Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="24923-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

