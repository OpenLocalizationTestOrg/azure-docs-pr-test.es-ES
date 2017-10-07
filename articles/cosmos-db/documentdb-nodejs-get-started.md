---
title: tutorial de aaaNode.js de hello API de documentos para la base de datos de Azure Cosmos | Documentos de Microsoft
description: Tutorial de Node.js que crea una base de datos de Cosmos con hello API de documentos.
keywords: tutorial de Node.js, base de datos de nodos
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Tutorial de Node.js: Hola Use API de documentos en la base de datos de Azure Cosmos toocreate una aplicación de consola Node.js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

¡Página principal del tutorial de Node.js de toohello de SDK de Node.js de base de datos de Azure Cosmos Hola! Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.

Describiremos:

* Creación y conexión de cuenta de base de datos de Azure Cosmos tooan
* Configuración de la aplicación
* Creación de una base de datos de nodos
* Creación de una colección
* Creación de documentos JSON
* Consultar la colección de Hola
* Sustitución de un documento
* Eliminación de un documento
* Eliminar base de datos de nodo de Hola

¿No tiene tiempo? ¡No se preocupe! está disponible en la solución completa de Hello [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Vea [obtener la solución completa de hello](#GetSolution) para obtener instrucciones rápidas.

Después de haber completado el tutorial de Node.js hello, por favor, use Hola botones de voto en hello superior e inferior de esta página toogive nos comentarios. Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios.

Comencemos.

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Requisitos previos para el tutorial de hello Node.js
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
    * Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.
* [Node.js](https://nodejs.org/) versión v0.10.29 o superior

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB
Vamos a crear una cuenta de Azure Cosmos DB. Si ya tiene una cuenta que desee toouse, puede pasar demasiado[configurar la aplicación Node.js](#SetupNode). Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la aplicación Node.js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Paso 2: Configuración de la aplicación de Node.js
1. Abra su terminal favorito.
2. Buscar carpeta de Hola o el directorio donde desea que toosave la aplicación Node.js.
3. Cree dos archivos de JavaScript vacíos con hello siguientes comandos:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Instalar el módulo de documentos de Hola a través de npm. Usar hello siguiente comando:
   * ```npm install documentdb --save```

Estupendo. Ahora que terminamos la configuración, comencemos a escribir algo de código.

## <a id="Config"></a>Paso 3: Configuración de las opciones de la aplicación
Abra ```config.js``` en el editor de texto que prefiera.

Entonces, copiar y pegar Hola siguiente fragmento de código y establecer las propiedades ```config.endpoint``` y ```config.primaryKey``` tooyour base de datos de Azure Cosmos uri de extremo y la clave principal. Ambos estas configuraciones pueden encontrarse en hello [portal de Azure](https://portal.azure.com).

![Tutorial de Node.js: captura de pantalla de portal de Azure, que muestra una cuenta de base de datos de Azure Cosmos, con centro activo Hola Hola resaltado, el botón de claves de hello resaltado en la hoja de cuenta de base de datos de Azure Cosmos Hola y Hola URI, valores de clave principal y la clave secundaria resaltados en hello Hoja de claves - base de datos de nodo][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Copie y pegue hello ```database id```, ```collection id```, y ```JSON documents``` tooyour ```config``` objeto siguiente donde se ha establecido la ```config.endpoint``` y ```config.authKey``` propiedades. Si ya tiene datos que le gustaría toostore en la base de datos, puede usar Azure Cosmos DB [herramienta de migración de datos](import-data.md) en lugar de agregar definiciones de documento de Hola.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Hello base de datos, la recopilación y definiciones de documento actuará como su base de datos de Azure Cosmos ```database id```, ```collection id```y los datos de documentos.

Por último, exportar la ```config``` objeto, por lo que puede hacer referencia en hello ```app.js``` archivo.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Paso 4: Conectar la cuenta de base de datos de Azure Cosmos tooan
Abra su vacío ```app.js``` archivo en el editor de texto hello. Copie y pegue el código de hello debajo de hello tooimport ```documentdb``` módulo y su recién creado ```config``` módulo.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Copie y pegue hello toouse Hola código que guardó anteriormente ```config.endpoint``` y ```config.primaryKey``` toocreate un DocumentClient nuevo.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Ahora que tiene el cliente de base de datos de Azure Cosmos de hello código tooinitialize hello, echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.

## <a name="step-5-create-a-node-database"></a>Paso 5: Creación de una base de datos de nodos
Copie y pegue el código de hello debajo de hello tooset código de estado HTTP para no se encuentra, la dirección url de base de datos de Hola y la dirección url de la colección de Hola. Estas direcciones URL son cómo encontrará el cliente de base de datos de Azure Cosmos Hola recopilación y base de datos derecho Hola.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) función de hello **DocumentClient** clase. Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos particionado entre colecciones.

Copie y pegue hello **getDatabase** función para crear la nueva base de datos de archivo de app.js de hello con hello ```id``` especificado en hello ```config``` objeto. Hello función comprobará si Hola de base de datos con hello mismo ```FamilyRegistry``` identificador ya no existe. Si existe, usaremos esa base de datos en lugar de crear una nueva.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copie y pegue el siguiente código de hello donde establecer hello **getDatabase** función función auxiliar de tooadd hello **salir** que imprimirán mensaje de bienvenida de salida y llamada de hello demasiado**getDatabase** (función).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

¡Enhorabuena! Ha creado correctamente una base de datos de Azure Cosmos DB.

## <a id="CreateColl"></a>Paso 6: Creación de una colección
> [!WARNING]
> **CreateDocumentCollectionAsync** creará una nueva colección, que tiene implicaciones de precios. Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) función de hello **DocumentClient** clase. Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.

Copie y pegue hello **getCollection** función debajo hello **getDatabase** funcionando en hello app.js archivo toocreate la nueva colección con hello ```id``` especificado en hello ```config```objeto. Una vez más, comprobaremos toomake seguro de que una colección de Hola mismo ```FamilyCollection``` identificador ya no existe. Si existe, usaremos esa colección en lugar de crear una nueva.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copie y pegue el código de hello debajo de llamada de hello demasiado**getDatabase** tooexecute hello **getCollection** (función).

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

¡Enhorabuena! Ha creado correctamente una colección de Azure Cosmos DB.

## <a id="CreateDoc"></a>Paso 7: Creación de un documento
A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) función de hello **DocumentClient** clase. Los documentos son contenido JSON definido por el usuario (arbitrario). Ahora puede insertar un documento en Azure Cosmos DB.

Copie y pegue hello **getFamilyDocument** función debajo hello **getCollection** función para crear documentos de Hola que contienen datos JSON de hello guardados en hello ```config``` objeto. Una vez más, comprobaremos toomake seguro de que un documento con hello mismo Id. no existe ya.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Copie y pegue el código de hello debajo de llamada de hello demasiado**getCollection** tooexecute hello **getFamilyDocument** (función).

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

¡Enhorabuena! Ha creado correctamente un documento de Azure Cosmos DB.

![Base de datos de tutorial: diagrama que ilustra la relación jerárquica de hello entre la cuenta de hello, base de datos de hello, colección de Hola y documentos de hello - nodo Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Paso 8: Consulta de los recursos de Azure Cosmos DB
Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones. Hello código de ejemplo siguiente muestra una consulta que se pueden ejecutar en documentos de hello en la colección.

Copie y pegue hello **queryCollection** función debajo hello **getFamilyDocument** función hello app.js archivo. Azure Cosmos DB admite consultas del tipo SQL tal y como se muestra a continuación. Para obtener más información sobre la creación de consultas complejas, desproteger hello [Query Playground](https://www.documentdb.com/sql/demo) hello y [consultar documentación](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


Hola siguiente diagrama ilustra cómo consulta de base de datos SQL de Azure Cosmos Hola sintaxis se llama en la colección de Hola que ha creado.

![Base de datos de tutorial: diagrama que ilustra el ámbito de Hola y lo que significa de consulta de hello - nodo Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Hola [FROM](documentdb-sql-query.md#FromClause) palabra clave es opcional en la consulta de hello porque las consultas de base de datos de Azure Cosmos ya están tooa ámbito sola colección. Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija. Base de datos de Azure Cosmos deducirá que familias, raíz o nombre de variable de hello eligió, referencia Hola colección actual de forma predeterminada.

Copie y pegue el código de hello debajo de llamada de hello demasiado**getFamilyDocument** tooexecute hello **queryCollection** (función).

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

¡Enhorabuena! Ha consultado correctamente documentos de Azure Cosmos DB.

## <a id="ReplaceDocument"></a>Paso 9: Reemplazo de un documento
Azure Cosmos DB admite la sustitución de documentos JSON.

Copie y pegue hello **replaceFamilyDocument** función debajo hello **queryCollection** función hello app.js archivo.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copie y pegue el código de hello debajo de llamada de hello demasiado**queryCollection** tooexecute hello **replaceDocument** (función). Además, agregue Hola código toocall **queryCollection** nuevo tooverify ese documento Hola tenía se cambió correctamente.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

¡Enhorabuena! Ha sustituido correctamente un documento de Azure Cosmos DB.

## <a id="DeleteDocument"></a>Paso 10: Eliminación de un documento
Azure Cosmos DB admite la eliminación de documentos JSON.

Copie y pegue hello **deleteFamilyDocument** función debajo hello **replaceFamilyDocument** (función).

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copie y pegue el código de hello debajo Hola llamada toohello en segundo lugar **queryCollection** tooexecute hello **deleteDocument** (función).

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

¡Enhorabuena! Ha eliminado correctamente un documento de Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Paso 11: Eliminar base de datos de nodo de Hola
Eliminando Hola creada la base de datos quitará la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).

Copie y pegue Hola **limpieza** función debajo Hola **deleteFamilyDocument** función de base de datos de tooremove hello y todos los recursos de los elementos secundarios de Hola.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Copie y pegue el código de hello debajo de llamada de hello demasiado**deleteFamilyDocument** tooexecute hello **limpieza** función.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Paso 12: Ejecute íntegramente la aplicación Node.js
Secuencia de Hola para llamar a las funciones debe ser similar al siguiente:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```

Debería ver la salida de hello de la aplicación iniciada get. salida de Hello debe coincidir con el texto de ejemplo de Hola a continuación.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

¡Enhorabuena! Ha creado se ha completado el tutorial de Node.js de Hola y tienen su primera aplicación de consola de base de datos de Azure Cosmos!

## <a id="GetSolution"></a>Obtener Hola completa Node.js solución del tutorial
Si no tiene tiempo toocomplete Hola pasos en este tutorial, o solo desea toodownload Hola código, puede obtenerlo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

solución GetStarted de hello toorun que contiene todos los ejemplos de hello en este artículo, se necesita Hola siguiente:

* [Cuenta de Azure Cosmos DB][create-account].
* Hola [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solución disponible en GitHub.

Instalar hello **documentdb** módulo a través de npm. Usar hello siguiente comando:

* ```npm install documentdb --save```

Después, en hello ```config.js``` archivo hello config.endpoint y config.authKey valores de actualización como se describe en [paso 3: establecer configuraciones de la aplicación](#Config). 

A continuación, en el terminal, busque su ```app.js``` y ejecute el comando hello: ```node app.js```.

Y, eso es todo, genérela y habrá terminado. 

## <a name="next-steps"></a>Pasos siguientes
* ¿Desea un ejemplo más complejo de Node.js? Consulte [Creación de una aplicación web de Node.js con Azure Cosmos DB](documentdb-nodejs-application.md).
* Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).
* Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).
* Obtener más información sobre el modelo de programación de Hola Hola sección desarrollar de hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
