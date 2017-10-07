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
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="5a439-104">Tutorial de Node.js: Hola Use API de documentos en la base de datos de Azure Cosmos toocreate una aplicación de consola Node.js</span><span class="sxs-lookup"><span data-stu-id="5a439-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a439-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5a439-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="5a439-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5a439-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="5a439-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="5a439-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="5a439-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a439-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="5a439-109">Java</span><span class="sxs-lookup"><span data-stu-id="5a439-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="5a439-110">C++</span><span class="sxs-lookup"><span data-stu-id="5a439-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="5a439-111">¡Página principal del tutorial de Node.js de toohello de SDK de Node.js de base de datos de Azure Cosmos Hola!</span><span class="sxs-lookup"><span data-stu-id="5a439-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="5a439-112">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="5a439-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="5a439-113">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="5a439-113">We'll cover:</span></span>

* <span data-ttu-id="5a439-114">Creación y conexión de cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="5a439-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="5a439-115">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5a439-115">Setting up your application</span></span>
* <span data-ttu-id="5a439-116">Creación de una base de datos de nodos</span><span class="sxs-lookup"><span data-stu-id="5a439-116">Creating a node database</span></span>
* <span data-ttu-id="5a439-117">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="5a439-117">Creating a collection</span></span>
* <span data-ttu-id="5a439-118">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="5a439-118">Creating JSON documents</span></span>
* <span data-ttu-id="5a439-119">Consultar la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="5a439-119">Querying hello collection</span></span>
* <span data-ttu-id="5a439-120">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="5a439-120">Replacing a document</span></span>
* <span data-ttu-id="5a439-121">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="5a439-121">Deleting a document</span></span>
* <span data-ttu-id="5a439-122">Eliminar base de datos de nodo de Hola</span><span class="sxs-lookup"><span data-stu-id="5a439-122">Deleting hello node database</span></span>

<span data-ttu-id="5a439-123">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="5a439-123">Don't have time?</span></span> <span data-ttu-id="5a439-124">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="5a439-124">Don't worry!</span></span> <span data-ttu-id="5a439-125">está disponible en la solución completa de Hello [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="5a439-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="5a439-126">Vea [obtener la solución completa de hello](#GetSolution) para obtener instrucciones rápidas.</span><span class="sxs-lookup"><span data-stu-id="5a439-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="5a439-127">Después de haber completado el tutorial de Node.js hello, por favor, use Hola botones de voto en hello superior e inferior de esta página toogive nos comentarios.</span><span class="sxs-lookup"><span data-stu-id="5a439-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="5a439-128">Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios.</span><span class="sxs-lookup"><span data-stu-id="5a439-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="5a439-129">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="5a439-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="5a439-130">Requisitos previos para el tutorial de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="5a439-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="5a439-131">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5a439-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="5a439-132">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5a439-132">An active Azure account.</span></span> <span data-ttu-id="5a439-133">Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a439-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="5a439-134">Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5a439-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="5a439-135">[Node.js](https://nodejs.org/) versión v0.10.29 o superior</span><span class="sxs-lookup"><span data-stu-id="5a439-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="5a439-136">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5a439-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="5a439-137">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="5a439-138">Si ya tiene una cuenta que desee toouse, puede pasar demasiado[configurar la aplicación Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="5a439-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="5a439-139">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la aplicación Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="5a439-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="5a439-140"><a id="SetupNode"></a>Paso 2: Configuración de la aplicación de Node.js</span><span class="sxs-lookup"><span data-stu-id="5a439-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="5a439-141">Abra su terminal favorito.</span><span class="sxs-lookup"><span data-stu-id="5a439-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="5a439-142">Buscar carpeta de Hola o el directorio donde desea que toosave la aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="5a439-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="5a439-143">Cree dos archivos de JavaScript vacíos con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="5a439-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="5a439-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="5a439-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="5a439-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="5a439-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="5a439-146">Instalar el módulo de documentos de Hola a través de npm.</span><span class="sxs-lookup"><span data-stu-id="5a439-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="5a439-147">Usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5a439-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="5a439-148">Estupendo.</span><span class="sxs-lookup"><span data-stu-id="5a439-148">Great!</span></span> <span data-ttu-id="5a439-149">Ahora que terminamos la configuración, comencemos a escribir algo de código.</span><span class="sxs-lookup"><span data-stu-id="5a439-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="5a439-150"><a id="Config"></a>Paso 3: Configuración de las opciones de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5a439-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="5a439-151">Abra ```config.js``` en el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="5a439-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="5a439-152">Entonces, copiar y pegar Hola siguiente fragmento de código y establecer las propiedades ```config.endpoint``` y ```config.primaryKey``` tooyour base de datos de Azure Cosmos uri de extremo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="5a439-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="5a439-153">Ambos estas configuraciones pueden encontrarse en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a439-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Tutorial de Node.js: captura de pantalla de portal de Azure, que muestra una cuenta de base de datos de Azure Cosmos, con centro activo Hola Hola resaltado, el botón de claves de hello resaltado en la hoja de cuenta de base de datos de Azure Cosmos Hola y Hola URI, valores de clave principal y la clave secundaria resaltados en hello Hoja de claves - base de datos de nodo][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="5a439-155">Copie y pegue hello ```database id```, ```collection id```, y ```JSON documents``` tooyour ```config``` objeto siguiente donde se ha establecido la ```config.endpoint``` y ```config.authKey``` propiedades.</span><span class="sxs-lookup"><span data-stu-id="5a439-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="5a439-156">Si ya tiene datos que le gustaría toostore en la base de datos, puede usar Azure Cosmos DB [herramienta de migración de datos](import-data.md) en lugar de agregar definiciones de documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a439-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

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


<span data-ttu-id="5a439-157">Hello base de datos, la recopilación y definiciones de documento actuará como su base de datos de Azure Cosmos ```database id```, ```collection id```y los datos de documentos.</span><span class="sxs-lookup"><span data-stu-id="5a439-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="5a439-158">Por último, exportar la ```config``` objeto, por lo que puede hacer referencia en hello ```app.js``` archivo.</span><span class="sxs-lookup"><span data-stu-id="5a439-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="5a439-159"><a id="Connect"></a>Paso 4: Conectar la cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="5a439-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="5a439-160">Abra su vacío ```app.js``` archivo en el editor de texto hello.</span><span class="sxs-lookup"><span data-stu-id="5a439-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="5a439-161">Copie y pegue el código de hello debajo de hello tooimport ```documentdb``` módulo y su recién creado ```config``` módulo.</span><span class="sxs-lookup"><span data-stu-id="5a439-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="5a439-162">Copie y pegue hello toouse Hola código que guardó anteriormente ```config.endpoint``` y ```config.primaryKey``` toocreate un DocumentClient nuevo.</span><span class="sxs-lookup"><span data-stu-id="5a439-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="5a439-163">Ahora que tiene el cliente de base de datos de Azure Cosmos de hello código tooinitialize hello, echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5a439-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="5a439-164">Paso 5: Creación de una base de datos de nodos</span><span class="sxs-lookup"><span data-stu-id="5a439-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="5a439-165">Copie y pegue el código de hello debajo de hello tooset código de estado HTTP para no se encuentra, la dirección url de base de datos de Hola y la dirección url de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a439-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="5a439-166">Estas direcciones URL son cómo encontrará el cliente de base de datos de Azure Cosmos Hola recopilación y base de datos derecho Hola.</span><span class="sxs-lookup"><span data-stu-id="5a439-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="5a439-167">A [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) función de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="5a439-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="5a439-168">Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos particionado entre colecciones.</span><span class="sxs-lookup"><span data-stu-id="5a439-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="5a439-169">Copie y pegue hello **getDatabase** función para crear la nueva base de datos de archivo de app.js de hello con hello ```id``` especificado en hello ```config``` objeto.</span><span class="sxs-lookup"><span data-stu-id="5a439-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="5a439-170">Hello función comprobará si Hola de base de datos con hello mismo ```FamilyRegistry``` identificador ya no existe.</span><span class="sxs-lookup"><span data-stu-id="5a439-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="5a439-171">Si existe, usaremos esa base de datos en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="5a439-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

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

<span data-ttu-id="5a439-172">Copie y pegue el siguiente código de hello donde establecer hello **getDatabase** función función auxiliar de tooadd hello **salir** que imprimirán mensaje de bienvenida de salida y llamada de hello demasiado**getDatabase** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

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

<span data-ttu-id="5a439-173">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-174">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-174">Congratulations!</span></span> <span data-ttu-id="5a439-175">Ha creado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="5a439-176"><a id="CreateColl"></a>Paso 6: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="5a439-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="5a439-177">**CreateDocumentCollectionAsync** creará una nueva colección, que tiene implicaciones de precios.</span><span class="sxs-lookup"><span data-stu-id="5a439-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="5a439-178">Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="5a439-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="5a439-179">A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) función de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="5a439-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="5a439-180">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5a439-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="5a439-181">Copie y pegue hello **getCollection** función debajo hello **getDatabase** funcionando en hello app.js archivo toocreate la nueva colección con hello ```id``` especificado en hello ```config```objeto.</span><span class="sxs-lookup"><span data-stu-id="5a439-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="5a439-182">Una vez más, comprobaremos toomake seguro de que una colección de Hola mismo ```FamilyCollection``` identificador ya no existe.</span><span class="sxs-lookup"><span data-stu-id="5a439-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="5a439-183">Si existe, usaremos esa colección en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="5a439-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

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

<span data-ttu-id="5a439-184">Copie y pegue el código de hello debajo de llamada de hello demasiado**getDatabase** tooexecute hello **getCollection** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5a439-185">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-186">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-186">Congratulations!</span></span> <span data-ttu-id="5a439-187">Ha creado correctamente una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="5a439-188"><a id="CreateDoc"></a>Paso 7: Creación de un documento</span><span class="sxs-lookup"><span data-stu-id="5a439-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="5a439-189">A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) función de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="5a439-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="5a439-190">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="5a439-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="5a439-191">Ahora puede insertar un documento en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="5a439-192">Copie y pegue hello **getFamilyDocument** función debajo hello **getCollection** función para crear documentos de Hola que contienen datos JSON de hello guardados en hello ```config``` objeto.</span><span class="sxs-lookup"><span data-stu-id="5a439-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="5a439-193">Una vez más, comprobaremos toomake seguro de que un documento con hello mismo Id. no existe ya.</span><span class="sxs-lookup"><span data-stu-id="5a439-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

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

<span data-ttu-id="5a439-194">Copie y pegue el código de hello debajo de llamada de hello demasiado**getCollection** tooexecute hello **getFamilyDocument** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5a439-195">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-196">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-196">Congratulations!</span></span> <span data-ttu-id="5a439-197">Ha creado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Base de datos de tutorial: diagrama que ilustra la relación jerárquica de hello entre la cuenta de hello, base de datos de hello, colección de Hola y documentos de hello - nodo Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="5a439-199"><a id="Query"></a>Paso 8: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5a439-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="5a439-200">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="5a439-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="5a439-201">Hello código de ejemplo siguiente muestra una consulta que se pueden ejecutar en documentos de hello en la colección.</span><span class="sxs-lookup"><span data-stu-id="5a439-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="5a439-202">Copie y pegue hello **queryCollection** función debajo hello **getFamilyDocument** función hello app.js archivo.</span><span class="sxs-lookup"><span data-stu-id="5a439-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="5a439-203">Azure Cosmos DB admite consultas del tipo SQL tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="5a439-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="5a439-204">Para obtener más información sobre la creación de consultas complejas, desproteger hello [Query Playground](https://www.documentdb.com/sql/demo) hello y [consultar documentación](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="5a439-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

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


<span data-ttu-id="5a439-205">Hola siguiente diagrama ilustra cómo consulta de base de datos SQL de Azure Cosmos Hola sintaxis se llama en la colección de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="5a439-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Base de datos de tutorial: diagrama que ilustra el ámbito de Hola y lo que significa de consulta de hello - nodo Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="5a439-207">Hola [FROM](documentdb-sql-query.md#FromClause) palabra clave es opcional en la consulta de hello porque las consultas de base de datos de Azure Cosmos ya están tooa ámbito sola colección.</span><span class="sxs-lookup"><span data-stu-id="5a439-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="5a439-208">Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="5a439-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="5a439-209">Base de datos de Azure Cosmos deducirá que familias, raíz o nombre de variable de hello eligió, referencia Hola colección actual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5a439-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="5a439-210">Copie y pegue el código de hello debajo de llamada de hello demasiado**getFamilyDocument** tooexecute hello **queryCollection** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5a439-211">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-212">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-212">Congratulations!</span></span> <span data-ttu-id="5a439-213">Ha consultado correctamente documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="5a439-214"><a id="ReplaceDocument"></a>Paso 9: Reemplazo de un documento</span><span class="sxs-lookup"><span data-stu-id="5a439-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="5a439-215">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="5a439-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="5a439-216">Copie y pegue hello **replaceFamilyDocument** función debajo hello **queryCollection** función hello app.js archivo.</span><span class="sxs-lookup"><span data-stu-id="5a439-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

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

<span data-ttu-id="5a439-217">Copie y pegue el código de hello debajo de llamada de hello demasiado**queryCollection** tooexecute hello **replaceDocument** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="5a439-218">Además, agregue Hola código toocall **queryCollection** nuevo tooverify ese documento Hola tenía se cambió correctamente.</span><span class="sxs-lookup"><span data-stu-id="5a439-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5a439-219">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-220">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-220">Congratulations!</span></span> <span data-ttu-id="5a439-221">Ha sustituido correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="5a439-222"><a id="DeleteDocument"></a>Paso 10: Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="5a439-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="5a439-223">Azure Cosmos DB admite la eliminación de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="5a439-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="5a439-224">Copie y pegue hello **deleteFamilyDocument** función debajo hello **replaceFamilyDocument** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

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

<span data-ttu-id="5a439-225">Copie y pegue el código de hello debajo Hola llamada toohello en segundo lugar **queryCollection** tooexecute hello **deleteDocument** (función).</span><span class="sxs-lookup"><span data-stu-id="5a439-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5a439-226">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-227">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-227">Congratulations!</span></span> <span data-ttu-id="5a439-228">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5a439-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="5a439-229"><a id="DeleteDatabase"></a>Paso 11: Eliminar base de datos de nodo de Hola</span><span class="sxs-lookup"><span data-stu-id="5a439-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="5a439-230">Eliminando Hola creada la base de datos quitará la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).</span><span class="sxs-lookup"><span data-stu-id="5a439-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="5a439-231">Copie y pegue Hola **limpieza** función debajo Hola **deleteFamilyDocument** función de base de datos de tooremove hello y todos los recursos de los elementos secundarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a439-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

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

<span data-ttu-id="5a439-232">Copie y pegue el código de hello debajo de llamada de hello demasiado**deleteFamilyDocument** tooexecute hello **limpieza** función.</span><span class="sxs-lookup"><span data-stu-id="5a439-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="5a439-233"><a id="Run"></a>Paso 12: Ejecute íntegramente la aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="5a439-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="5a439-234">Secuencia de Hola para llamar a las funciones debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="5a439-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="5a439-235">En el terminal, busque su ```app.js``` y ejecute el comando hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5a439-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="5a439-236">Debería ver la salida de hello de la aplicación iniciada get.</span><span class="sxs-lookup"><span data-stu-id="5a439-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="5a439-237">salida de Hello debe coincidir con el texto de ejemplo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="5a439-237">hello output should match hello example text below.</span></span>

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

<span data-ttu-id="5a439-238">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5a439-238">Congratulations!</span></span> <span data-ttu-id="5a439-239">Ha creado se ha completado el tutorial de Node.js de Hola y tienen su primera aplicación de consola de base de datos de Azure Cosmos!</span><span class="sxs-lookup"><span data-stu-id="5a439-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="5a439-240"><a id="GetSolution"></a>Obtener Hola completa Node.js solución del tutorial</span><span class="sxs-lookup"><span data-stu-id="5a439-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="5a439-241">Si no tiene tiempo toocomplete Hola pasos en este tutorial, o solo desea toodownload Hola código, puede obtenerlo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="5a439-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="5a439-242">solución GetStarted de hello toorun que contiene todos los ejemplos de hello en este artículo, se necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="5a439-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="5a439-243">[Cuenta de Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="5a439-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="5a439-244">Hola [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solución disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a439-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="5a439-245">Instalar hello **documentdb** módulo a través de npm.</span><span class="sxs-lookup"><span data-stu-id="5a439-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="5a439-246">Usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5a439-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="5a439-247">Después, en hello ```config.js``` archivo hello config.endpoint y config.authKey valores de actualización como se describe en [paso 3: establecer configuraciones de la aplicación](#Config).</span><span class="sxs-lookup"><span data-stu-id="5a439-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="5a439-248">A continuación, en el terminal, busque su ```app.js``` y ejecute el comando hello: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="5a439-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="5a439-249">Y, eso es todo, genérela y habrá terminado.</span><span class="sxs-lookup"><span data-stu-id="5a439-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5a439-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a439-250">Next steps</span></span>
* <span data-ttu-id="5a439-251">¿Desea un ejemplo más complejo de Node.js?</span><span class="sxs-lookup"><span data-stu-id="5a439-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="5a439-252">Consulte [Creación de una aplicación web de Node.js con Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="5a439-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="5a439-253">Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="5a439-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="5a439-254">Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="5a439-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="5a439-255">Obtener más información sobre el modelo de programación de Hola Hola sección desarrollar de hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="5a439-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
