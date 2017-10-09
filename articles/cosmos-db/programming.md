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
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Programación en el servidor de Azure Cosmos DB: procedimientos almacenados, desencadenadores de base de datos y funciones definidas por el usuario
Conozca cómo la ejecución transaccional integrada del lenguaje de Azure Cosmos DB de JavaScript permite a los desarrolladores escribir **procedimientos almacenados**, **desencadenadores** y **funciones definidas por el usuario (UDF)** de forma nativa en un elemento de JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/). Esto le permite toowrite lógica de aplicación de programa de base de datos que puede distribuir y ejecutarse directamente en las particiones de almacenamiento de base de datos de Hola. 

Le recomendamos que obtenga iniciada por ver Hola después de vídeo, donde Andrew Liu proporciona un tooCosmos breve introducción de la base de datos modelo de programación de base de datos de servidor. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

A continuación, devolver artículo toothis, donde obtendrá información sobre Hola respuestas toohello siguientes preguntas:  

* ¿Cómo se escribe un procedimiento almacenado, un desencadenador o una UDF con JavaScript?
* ¿Qué garantías ACID ofrece Cosmos DB?
* ¿Cómo funcionan las transacciones en Cosmos DB?
* ¿Qué son los desencadenadores previos y posteriores y cómo se escriben?
* ¿Cómo se registran y se ejecutan un procedimiento almacenado, un desencadenador o una UDF de forma compatible con REST mediante HTTP?
* ¿Las Cosmos DB SDK toocreate disponible y ejecutar procedimientos almacenados, desencadenadores y UDF?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Introducción tooStored procedimiento y la programación de UDF
Este enfoque de *"JavaScript como un día moderno T-SQL"* evita que los desarrolladores de aplicaciones de las complejidades de Hola de discordancias del sistema y las tecnologías de asignación objeto-relacional. También tiene una serie de ventajas intrínsecas que pueden ser utilizados toobuild completas aplicaciones:  

* **Lógica de procedimientos:** JavaScript como un lenguaje de programación de alto nivel, proporciona una interfaz enriquecida y familiar tooexpress lógica de negocios. Puede realizar complejas secuencias de datos de toohello más cerca de las operaciones.
* **Transacciones atómicas:** Cosmos DB garantiza que las operaciones de base de datos realizadas dentro de un único procedimiento almacenado o desencadenador sean atómicas. Esto permite a una aplicación combinar operaciones relacionadas en un único lote para que todas se realicen correctamente o no lo haga ninguna. 
* **Rendimiento:** hecho de Hola que JSON es intrínsecamente asignadas toohello Javascript language type system y es también la unidad básica de Hola de almacenamiento en la base de datos de Cosmos permite un número de optimizaciones como diferida materialización de JSON se documenta en el búfer de Hola grupo y dejándolos disponible toohello petición ejecutar código. Hay más ventajas de rendimiento asociados a la base de datos toohello lógica de negocios trasvase:
  
  * Procesamiento por lotes: los desarrolladores pueden agrupar operaciones como inserciones y enviarlas en masa. costo de latencia de tráfico de red de Hola y transacciones independientes de hello almacén toocreate sobrecarga se reducción significativamente. 
  * Precompilación: Cosmos DB precompila procedimientos almacenados, desencadenadores y definidos por el usuario (UDF) funciones tooavoid costo de compilación de JavaScript para cada invocación. Hello sobrecarga de la generación de código de bytes de hello para la lógica de procedimientos de hello es había amortizado tooa un valor mínimo.
  * Secuenciación: muchas operaciones necesitan un efecto secundario (“desencadenador”) que implica potencialmente realizar una o más operaciones de almacenamiento secundarias. Además de atomicidad, esto tiene un mejor rendimiento al mover servidor toohello. 
* **Encapsulación:** procedimientos almacenados pueden ser utilizados toogroup lógica de negocios en un solo lugar. Esto tiene dos ventajas:
  * Agrega una capa de abstracción sobre los datos sin procesar de hello, que permite que sus aplicaciones independientemente de los datos de hello tooevolve arquitectos de datos. Esto es especialmente ventajoso cuando Hola datos sin esquema debido toohello suposiciones complicado que necesitan toobe incrustada en la aplicación hello si tienen toodeal con datos directamente.  
  * Esta abstracción permite a las empresas proteger sus datos mediante la optimización de acceso de Hola desde scripts de Hola.  

Hello creación y ejecución de desencadenadores de base de datos, procedimiento almacenado y operadores de consulta personalizada se admite a través de hello [API de REST](/rest/api/documentdb/), [estudio de DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases), y [SDKdecliente](documentdb-sdk-dotnet.md) en numerosas plataformas incluidas. NET, Node.js y JavaScript.

Este tutorial usa hello [SDK de Node.js con preguntas promesas](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sintaxis y el uso de procedimientos almacenados, desencadenadores y UDF.   

## <a name="stored-procedures"></a>Procedimientos almacenados
### <a name="example-write-a-simple-stored-procedure"></a>Ejemplo: creación de un procedimiento almacenado sencillo
Comencemos con un sencillo procedimiento almacenado que devuelve una respuesta “Hello World”.

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Los procedimientos almacenados se registran por colección y pueden funcionar en cualquier documento y dato adjunto presente en esa colección. Hello fragmento de código siguiente muestra cómo tooregister Hola helloWorld procedimiento almacenado con una colección. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Una vez que se registra el procedimiento almacenado de hello, podemos ejecutar con la colección de Hola y leer los resultados de hello en el cliente de Hola. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


objeto de contexto de Hello proporciona acceso tooall operaciones que pueden realizarse en el almacenamiento de base de datos de Cosmos, así como tener acceso a los objetos de solicitud y respuesta de toohello. En este caso, hemos usado Hola respuesta tooset Hola el cuerpo del objeto de respuesta de Hola que envió el cliente toohello atrás. Para obtener más información, consulte toohello [server documentación del SDK de Azure Cosmos DB JavaScript](http://azure.github.io/azure-documentdb-js-server/).  

Permítanos ampliar este ejemplo y agregar más funciones relacionadas con la base de datos toohello de procedimiento almacenado. Los procedimientos almacenados pueden crear, actualizar, leer, consultar y eliminar los documentos y datos adjuntos dentro de la colección de Hola.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Ejemplo: Escribir un procedimiento almacenado toocreate un documento
el fragmento siguiente de Hello muestra cómo toouse Hola toointeract del objeto de contexto con recursos de base de datos de Cosmos.

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


Este procedimiento almacenado toma como entrada documentToCreate, cuerpo de Hola de un toobe documento creado en la colección actual de Hola. Todas estas operaciones son asíncronas y dependen de las devoluciones de llamadas de función de JavaScript. función de devolución de llamada de Hello tiene dos parámetros, uno para el objeto de error de hello en caso de que se produce un error en la operación de Hola y uno para hello creó el objeto. Dentro de la devolución de llamada de hello, los usuarios pueden controlar la excepción de Hola o producir un error. En caso de que no se proporciona una devolución de llamada y se produce un error, el tiempo de ejecución de base de datos de Azure Cosmos Hola produce un error.   

En el ejemplo de Hola anterior, devolución de llamada de hello produce un error si el error en la operación de Hola. En caso contrario, Establece Id. de Hola de hello creado el documento como cuerpo del mensaje del cliente de toohello de respuesta de Hola Hola. A continuación se explica cómo se ejecuta este procedimiento almacenado con parámetros de entrada.

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


Tenga en cuenta que este procedimiento almacenado puede ser modificado tootake una matriz de los cuerpos de documento como entrada y crearlos en hello mismo almacenado ejecución del procedimiento en lugar de la red varias solicitudes toocreate de ellos individualmente. Esto puede ser usado tooimplement un importador masiva eficaz para la base de datos de Cosmos (se explica más adelante en este tutorial).   

ejemplo de Hola descrito muestra cómo procedimientos almacenados del toouse. Desencadenadores y funciones definidas por el usuario (UDF) se explica más adelante en el tutorial Hola.

## <a name="database-program-transactions"></a>Transacciones del programa de base de datos
Una transacción en una base de datos típica se puede definir como una secuencia de operaciones realizadas como una única unidad lógica de trabajo. Cada transacción proporciona **garantías ACID**. ACID es un acrónimo conocido que, por sus siglas en inglés, hace referencia a cuatro propiedades: Atomicidad, Coherencia, Aislamiento y Durabilidad.  

En pocas palabras, la atomicidad garantiza que todo el trabajo Hola realizado dentro de una transacción se trata como una sola unidad donde cualquier toda ella se confirma o ninguno. Coherencia se asegura de que los datos de hello siempre están en buen estado interno a través de las transacciones. Aislamiento garantiza que no haya dos transacciones interfieren entre sí: por lo general, más comerciales sistemas proporcionan varios niveles de aislamiento que se pueden usar en función de las necesidades de aplicación Hola. Durabilidad se garantiza que cualquier cambio que se confirma en la base de datos de hello siempre estará presente.   

En la base de datos de Cosmos, JavaScript se hospeda en hello mismo espacio de memoria como base de datos de Hola. Por lo tanto, las solicitudes realizadas dentro de procedimientos almacenados y desencadenadores ejecutan en hello mismo ámbito de una sesión de base de datos. Esto permite Cosmos DB tooguarantee ACID para todas las operaciones que forman parte de un único procedimiento almacenado o desencadenador. Tenga en cuenta los siguiente Hola almacena la definición del procedimiento:

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

Este procedimiento almacenado usa transacciones en un juego aplicación tootrade de los elementos entre dos jugadores en una sola operación. Hola almacenado cada jugador toohello correspondiente identificadores pasa como un argumento de procedimiento intentos tooread dos documentos. Si se encuentran ambos documentos Reproductor, procedimiento almacenado de hello actualiza documentos Hola intercambiando sus elementos. Si se detectan errores durante el proceso de hello, produce una excepción de JavaScript que implícitamente anula la transacción de Hola.

Si hello procedimiento Hola almacenado de recopilación se ha registrado con es una colección única partición, entonces transacción hello es tooall ámbito Hola documentos dentro de la colección de Hola. Si la colección de hello tiene particiones, los procedimientos almacenados se ejecutan en el ámbito de transacción de Hola de una clave de partición única. Cada uno de ellos almacenados de ejecución del procedimiento, a continuación, debe incluir un valor de clave de partición debe ejecutarse toohello ámbito hello de la transacción correspondiente en. Para más información, consulte [Creación de particiones con Azure Cosmos DB](partition-data.md).

### <a name="commit-and-rollback"></a>Confirmación y reversión
Las transacciones están integradas de forma profunda y nativa en el modelo de programación de JavaScript de Cosmos DB. Dentro de una función de JavaScript, todas las operaciones se ajustan automáticamente en una única transacción. Si hello JavaScript finalice sin ninguna excepción, base de datos de hello operations toohello se confirman. En efecto, las instrucciones de "BEGIN TRANSACTION" y "COMMIT TRANSACTION" hello en bases de datos relacionales están implícitas en base de datos de Cosmos.  

Si se produce cualquier excepción que se propaga desde el script de Hola, tiempo de ejecución de JavaScript de Cosmos DB revertirá toda transacción de Hola. Como se muestra en hello anteriormente ejemplo, producir una excepción es realmente el equivalente tooa "ROLLBACK TRANSACTION" en la base de datos de Cosmos.

### <a name="data-consistency"></a>Coherencia de datos
Desencadenadores y procedimientos almacenados se ejecutan siempre en la réplica principal de Hola de contenedor de base de datos de Azure Cosmos Hola. Esto garantiza que las lecturas desde dentro de los procedimientos almacenados ofrecen una fuerte coherencia. Se pueden ejecutar consultas con funciones definidas por el usuario en Hola principal o cualquier réplica secundaria, pero asegúrese de toomeet Hola solicitado nivel de coherencia eligiendo réplica adecuado Hola.

## <a name="bounded-execution"></a>Ejecución vinculada
Todas las operaciones de base de datos de Cosmos deben completarse dentro de servidor hello especificado duración de tiempo de espera de la solicitud. Esta restricción también aplica a las funciones de tooJavaScript (procedimientos almacenados, desencadenadores y funciones definidas por el usuario). Si no completó una operación con ese límite de tiempo, se revierten las transacciones de Hola. Funciones de JavaScript deben finalizó dentro del límite de tiempo de Hola o implementar una continuación según modelar toobatch/reanudar la ejecución.  

En el desarrollo de toosimplify orden almacenado procedimientos y desencadenadores toohandle límites de tiempo, todas las funciones en el objeto de colección de hello (para crear, leer, reemplazar y eliminación de documentos y datos adjuntos) devuelven un valor booleano que representa si la operación se completó. Si este valor es false, es una indicación que límite de tiempo de hello es sobre tooexpire y ese procedimiento Hola debe contener la ejecución.  Operaciones en cola toohello previa la primera operación de almacén no aceptado se garantizan toocomplete si procedimiento almacenado de hello completa en el tiempo y no en cola las solicitudes más.  

Las funciones de JavaScript también se vinculan al consumo de recursos. COSMOS DB reserva el rendimiento por la colección basándose en el tamaño de hello aprovisionado de una cuenta de base de datos. La capacidad de proceso se expresa en términos de una unidad de CPU normalizada, consumo de memoria y E/S llamadas unidades de solicitud o RU. Funciones de JavaScript potencialmente pueden utilizar un gran número de RUs en poco tiempo y podrían obtener velocidad limitado si se alcanza el límite de la colección de Hola. Procedimientos almacenados de uso intensivo de recursos también pueden ser disponibilidad tooensure en cuarentena de operaciones de base de datos primitivo.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Ejemplo: importación masiva de datos a un programa de base de datos
A continuación se muestra un ejemplo de un procedimiento almacenado que se escribe toobulk importar documentos en una colección. Tenga en cuenta cómo Hola almacena la ejecución del procedimiento identificadores limitados activando Hola booleano devolver valor de createDocument y, a continuación, utiliza Hola número de documentos que se insertan en cada invocación del procedimiento tootrack y reanudar progreso de hello almacenado en lotes.

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

## <a id="trigger"></a> Desencadenadores de base de datos
### <a name="database-pre-triggers"></a>Desencadenadores previos de base de datos
Cosmos DB proporciona desencadenadores que se ejecutan o desencadenan por una operación en un documento. Por ejemplo, puede especificar un desencadenador anterior cuando está creando un documento: este desencadenador anterior se ejecutará antes de que se crea el documento de Hola. Hola te mostramos un ejemplo de cómo desencadenadores previos pueden ser usado toovalidate Hola propiedades de un documento que se va a crear:

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


Hello correspondiente código de registro del lado cliente de Node.js para un desencadenador de Hola y:

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


Los desencadenadores previos no pueden tener parámetros de entrada. objeto de solicitud de Hello puede ser el mensaje de solicitud de hello toomanipulate utilizados asociado a la operación de Hola. En este caso, desencadenador previo Hola se ejecuta con la creación de hello de un documento y cuerpo del mensaje de solicitud de hello contiene Hola documento toobe creado en formato JSON.   

Cuando se registren los desencadenadores, los usuarios pueden especificar operaciones de Hola que se pueden ejecutar con. Este desencadenador se creó con TriggerOperation.Create, lo que significa que no se permite la continuación de Hola.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Desencadenadores anteriores de base de datos
Los desencadenadores posteriores, del mismo modo que los previos, se asocian con una operación de un documento y no aceptan parámetros de entrada. Se ejecutan **después** Hola operación se ha completado y tiene el mensaje de respuesta de toohello de acceso que se envía el cliente toohello.   

Hola siguiente ejemplo muestra los desencadenadores posteriores en acción:

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


desencadenador de Hola se puede registrar como se muestra en el siguiente ejemplo de Hola.

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


Este desencadenador consulta documento de metadatos de Hola y actualiza con detalles sobre el documento de hello recién creado.  

Algo que es importante toonote es hello **transaccional** ejecución de desencadenadores en la base de datos de Cosmos. Este desencadenador posterior a la que se ejecuta como parte del programa Hola misma transacción como la creación de hello del documento original de Hola. Por lo tanto, si se produce una excepción del desencadenador posterior a la de hello (por ejemplo si estamos documento de metadatos de hello no se puede tooupdate), transacción entera Hola se producirá un error y se revierte. No se creará ningún documento y se devolverá una excepción.  

## <a id="udf"></a>Funciones definidas por el usuario
Funciones definidas por el usuario (UDF) son la gramática del lenguaje de consulta de tooextend usado Hola documentos API SQL e implementan lógica de negocios personalizada. Solo se las puede llamar desde consultas internas. Que no tiene el objeto de contexto de acceso toohello y sirven de toobe utilizado como JavaScript solo proceso. Por lo tanto, se pueden ejecutar UDF en las réplicas secundarias de hello servicio base de datos de Cosmos.  

Hello en el ejemplo siguiente crea un UDF toocalculate impuesto, basándose en las tasas para distintos corchetes de ingresos y, a continuación, lo usa dentro de una consulta toofind todas las personas que más de 20.000 $ de pago de impuestos.

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


Hola UDF puede utilizarse posteriormente en las consultas como en el siguiente ejemplo de Hola:

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

## <a name="javascript-language-integrated-query-api"></a>API de consulta integradas en lenguajes JavaScript
Además tooissuing consultas con la gramática SQL de DocumentDB, hello servidor SDK permiten consultas tooperform optimizado mediante una interfaz de JavaScript fluida sin ningún conocimiento de SQL. consulta de JavaScript de Hello que API permite tooprogrammatically compilación consultas al pasar las funciones de predicado a la función encadenable llama, con un tooECMAScript5 familiar sintaxis elementos integrados de matriz y populares bibliotecas de JavaScript como lodash. Hola JavaScript en tiempo de ejecución toobe ejecutado eficazmente con índices de Azure Cosmos DB analiza las consultas.

> [!NOTE]
> `__`(doble subrayado) es un alias demasiado`getContext().getCollection()`.
> <br/>
> En otras palabras, puede usar `__` o `getContext().getCollection()` tooaccess Hola API de consulta de JavaScript.
> 
> 

Estas son algunas de las funciones compatibles:

<ul>
<li>
<b>chain() ... .value([callback] [, options])</b>
<ul>
<li>
Inicia una llamada encadenada que debe terminarse con value().
</li>
</ul>
</li>
<li>
<b>filter(predicateFunction [, options] [, callback])</b>
<ul>
<li>
Filtra hello mediante una función de predicado que devuelve true o false en orden toofilter documentos de entrada de entrada/salida en el conjunto resultante de Hola de entrada. Este comportamiento es similar tooa cláusula WHERE de SQL.
</li>
</ul>
</li>
<li>
<b>map(transformationFunction [, options] [, callback])</b>
<ul>
<li>
Se aplica una proyección dada una función de transformación que se asigna cada objeto de JavaScript de tooa de elemento de entrada o valor. Este comportamiento es similar cláusula SELECT tooa en SQL.
</li>
</ul>
</li>
<li>
<b>pluck([propertyName] [, options] [, callback])</b>
<ul>
<li>
Se trata de un método abreviado de un mapa que extrae el valor de Hola de una propiedad única de cada elemento de entrada.
</li>
</ul>
</li>
<li>
<b>flatten([isShallow] [, options] [, callback])</b>
<ul>
<li>
Combina y reduce las matrices de cada elemento de entrada de matriz único tooa. Este comportamiento es similar tooSelectMany en LINQ.
</li>
</ul>
</li>
<li>
<b>sortBy([predicate] [, options] [, callback])</b>
<ul>
<li>
Generar un nuevo conjunto de documentos de ordenación de los documentos de hello en secuencia de documento de entrada de hello en orden ascendente mediante Hola dado el predicado. Este comportamiento es similar tooa cláusula ORDER BY de SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending([predicate] [, options] [, callback])</b>
<ul>
<li>
Generar un nuevo conjunto de documentos de ordenación de los documentos de hello en secuencia de documento de entrada de hello en orden descendente mediante Hola dado el predicado. Este comportamiento es similar tooa ORDER BY x DESC cláusula de SQL.
</li>
</ul>
</li>
</ul>


Cuando se incluye dentro de las funciones de predicado o selector, hello siguientes construcciones de JavaScript obtener automáticamente optimizado toorun directamente en la base de datos de Azure Cosmos índices:

* Operadores simples: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Literales, incluidos el literal de objeto hello: {}
* var, return

Hola JavaScript siguiente construye no obtener optimizada para los índices de base de datos de Azure Cosmos:

* Control de flujo (por ejemplo: if, for, while)
* Llamadas a funciones

Para obtener más información, consulte [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Ejemplo: Escribir un procedimiento almacenado mediante la API de consulta de JavaScript de Hola
Hola siguiendo el ejemplo de código es un ejemplo de cómo puede usarse Hola API de consulta de JavaScript en el contexto de Hola de un procedimiento almacenado. Inserta un documento, proporcionado por un parámetro de entrada, Hello procedimiento almacenado y actualiza un documento de metadatos, mediante hello `__.filter()` método con minSize, maxSize y totalSize en función de la propiedad de tamaño del documento entrada Hola.

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

## <a name="sql-toojavascript-cheat-sheet"></a>Hoja de referencia SQL tooJavascript
Hello tabla siguiente presenta varias consultas SQL y las consultas de JavaScript correspondientes Hola.

Como sucede con las consultas SQL, las claves de propiedad del documento (por ejemplo, `doc.id`) distinguen mayúsculas de minúsculas.

|SQL| API de consulta de JavaScript|Descripción siguiente|
|---|---|---|
|SELECT *<br>FROM docs| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;return doc;<br>});|1|
|SELECT docs.id, docs.message AS msg, docs.actions <br>FROM docs|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;actions:doc.actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECT *<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>});|3|
|SELECT *<br>FROM docs<br>WHERE ARRAY_CONTAINS(docs.Tags, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags &amp;&amp; x.Tags.indexOf(123) &gt; -1;<br>});|4|
|SELECT docs.id, docs.message AS msg<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.id ==="X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.value();|5|
|SELECT VALUE tag<br>FROM docs<br>JOIN tag IN docs.Tags<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.Tags &amp;&amp; Array.isArray(doc.Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.value()|6|

Hello las descripciones siguientes explican cada consulta en la tabla de hello anterior.
1. Devuelve resultados de todos los documentos (paginados con el token de continuación) tal y como están.
2. Id. de Hola de proyectos, mensaje (alias toomsg) y acción de todos los documentos.
3. Las consultas para los documentos con predicado hello: id = "X998_Y998".
4. Las consultas para los documentos que tengan una propiedad de etiquetas y etiquetas es una matriz que contiene el valor de hello 123.
5. Las consultas para los documentos con un predicado, id = "X998_Y998" y, a continuación, Id. de Hola de proyectos y mensajes (con alias toomsg).
6. Filtra los documentos que tienen una propiedad de matriz, etiquetas, y ordena los documentos resultantes Hola por propiedad del sistema de hello _ts marca de tiempo y a continuación, proyecta + aplana la matriz de etiquetas de Hola.


## <a name="runtime-support"></a>Compatibilidad con el tiempo de ejecución
[API de lado de servidor de DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) Hola proporciona compatibilidad con la mayoría de hello principales características del lenguaje JavaScript como normalizado por [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Seguridad
JavaScript procedimientos almacenados y desencadenadores son en recintos de seguridad para que los efectos de Hola de una secuencia de comandos no pierden toohello otro sin tener que pasar a través de aislamiento de transacción de instantánea de hello en el nivel de base de datos de Hola. entornos de tiempo de ejecución de Hello están agrupados pero se limpian del contexto de hello después de cada ejecución. Por lo tanto, garantiza que sean toobe seguro para la ejecución de los efectos secundarios imprevistos entre sí.

### <a name="pre-compilation"></a>Precompilación
Los procedimientos almacenados, desencadenadores y UDF son implícitamente precompilado toohello formato de código de bytes en el costo de compilación de orden tooavoid en tiempo de Hola de cada invocación del script. Esto garantiza que las invocaciones de los procedimientos almacenados son rápidos y tienen poca superficie.

## <a name="client-sdk-support"></a>Compatibilidad con SDK de cliente
En suma toohello API de documentos para [Node.js](documentdb-sdk-node.md) cliente, base de datos de Azure Cosmos tiene [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), y [SDK de Python](documentdb-sdk-python.md) para hello API de documentos. Los procedimientos almacenados, desencadenadores y UDF también se pueden crear y ejecutar mediante cualquiera de estos SDK. Hola siguiente ejemplo se muestra cómo toocreate y ejecutar un procedimiento almacenado mediante el cliente de .NET de Hola. Tenga en cuenta cómo se pasan los tipos de .NET de hello en hello procedimiento almacenado como JSON y lea el contenido.

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


Este ejemplo se muestra cómo hello toouse [API de .NET de DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate un desencadenador anterior y crear un documento con desencadenador Hola habilitado. 

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


Y Hola de ejemplo siguiente muestra cómo define las toocreate un usuario (UDF) de la función y usarlo en un [consulta documentos API SQL](documentdb-sql-query.md).

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

## <a name="rest-api"></a>API de REST
Todas las operaciones de Azure Cosmos DB se pueden realizar mediante RESTful. Los procedimientos almacenados, desencadenadores y funciones definidas por el usuario se pueden registrar en una colección mediante POST HTTP. Hello aquí te mostramos un ejemplo de cómo tooregister un procedimiento almacenado:

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


Hello procedimiento almacenado se ha registrado mediante la ejecución de una solicitud POST contra Hola URI bases de datos/testdb/colls/testColl/sprocs Hola cuerpo que contenga Hola toocreate de procedimiento almacenado. Los desencadenadores y las UDF se pueden registrar de forma similar mediante la emisión de una solicitud POST con respecto a /triggers y /udfs, respectivamente.
Este procedimiento almacenado se puede ejecutar mediante la emisión de una solicitud POST en su vínculo de recursos:

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


En este caso, se pasa al procedimiento toohello entrada almacenado Hola Hola del cuerpo de solicitud. Tenga en cuenta que la entrada de Hola se pasa como una matriz JSON de parámetros de entrada. Hola almacena la primera entrada de procedimiento toma Hola como un documento que forma un cuerpo de respuesta. respuesta de Hola que recibimos es como sigue:

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


Los desencadenadores, a diferencia de los procedimientos almacenados, no se pueden ejecutar directamente. En su lugar, se ejecutan como parte de una operación en un documento. Podemos especificar Hola desencadenadores toorun con una solicitud mediante encabezados HTTP. Hola aquí te mostramos toocreate un documento de solicitud.

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


Aquí se especifica Hola desencadenador previo toobe ejecutar con la solicitud de hello en encabezado x-ms-documentdb-pre-trigger-include Hola. En consecuencia, los desencadenadores posteriores se proporcionan en encabezado x-ms-documentdb-post-trigger-include Hola. Tenga en cuenta que tanto los desencadenadores previos como los posteriores se pueden especificar para una solicitud determinada.

## <a name="sample-code"></a>Código de ejemplo
Puede encontrar más ejemplos de código del lado servidor (entre los que se incluyen [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) y [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) en nuestro [repositorio de GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

¿Desea que el procedimiento almacenado Maravilla tooshare? Envíenos una solicitud de extracción. 

## <a name="next-steps"></a>Pasos siguientes
Una vez que tenga uno o más procedimientos almacenados, desencadenadores y funciones definidas por el usuario creadas, puede cargarlos y verlos en hello portal de Azure mediante el Explorador de datos.

También puede buscar siguiente Hola referencias y recursos útiles para su toolearn de ruta de acceso más información acerca de la programación del servidor de base de datos de Azure Cosmos:

* [SDK de Azure Cosmos DB](documentdb-sdk-dotnet.md)
* [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Extensibilidad de la base de datos segura y portátil](http://dl.acm.org/citation.cfm?id=276339) 
* [Arquitectura de base de datos orientada a servicios](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Hola de hospedaje en tiempo de ejecución de .NET en Microsoft SQL server](http://dl.acm.org/citation.cfm?id=1007669)

