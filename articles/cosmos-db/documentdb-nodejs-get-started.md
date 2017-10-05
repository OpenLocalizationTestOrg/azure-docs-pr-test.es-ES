---
title: Tutorial de Node.js para la API de DocumentDB de Azure Cosmos DB | Microsoft Docs
description: Tutorial de Node.js en el que se crea una instancia de Cosmos DB con la API de DocumentDB.
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
ms.openlocfilehash: 6510e0270bb2efa252a2b2ad40014c5d26b74a81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-tutorial-use-the-documentdb-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="d119a-104">Tutorial de Node.js: utilización de la API de DocumentDB en Azure Cosmos DB para crear una aplicación de consola Node.js</span><span class="sxs-lookup"><span data-stu-id="d119a-104">Node.js tutorial: Use the DocumentDB API in Azure Cosmos DB to create a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d119a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d119a-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="d119a-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d119a-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="d119a-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="d119a-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="d119a-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="d119a-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="d119a-109">Java</span><span class="sxs-lookup"><span data-stu-id="d119a-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="d119a-110">C++</span><span class="sxs-lookup"><span data-stu-id="d119a-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="d119a-111">Le damos la bienvenida al tutorial de Node.js para el SDK de Node.js de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="d119a-112">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="d119a-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="d119a-113">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="d119a-113">We'll cover:</span></span>

* <span data-ttu-id="d119a-114">Creación de una cuenta de Azure Cosmos DB y conexión a ella</span><span class="sxs-lookup"><span data-stu-id="d119a-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="d119a-115">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d119a-115">Setting up your application</span></span>
* <span data-ttu-id="d119a-116">Creación de una base de datos de nodos</span><span class="sxs-lookup"><span data-stu-id="d119a-116">Creating a node database</span></span>
* <span data-ttu-id="d119a-117">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="d119a-117">Creating a collection</span></span>
* <span data-ttu-id="d119a-118">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="d119a-118">Creating JSON documents</span></span>
* <span data-ttu-id="d119a-119">Consulta de la colección</span><span class="sxs-lookup"><span data-stu-id="d119a-119">Querying the collection</span></span>
* <span data-ttu-id="d119a-120">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="d119a-120">Replacing a document</span></span>
* <span data-ttu-id="d119a-121">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="d119a-121">Deleting a document</span></span>
* <span data-ttu-id="d119a-122">Eliminación de la base de datos de nodos</span><span class="sxs-lookup"><span data-stu-id="d119a-122">Deleting the node database</span></span>

<span data-ttu-id="d119a-123">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="d119a-123">Don't have time?</span></span> <span data-ttu-id="d119a-124">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="d119a-124">Don't worry!</span></span> <span data-ttu-id="d119a-125">La solución completa está disponible en [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d119a-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="d119a-126">Consulte [Obtención de la solución completa](#GetSolution) para obtener instrucciones rápidas.</span><span class="sxs-lookup"><span data-stu-id="d119a-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="d119a-127">Después de haber completado el tutorial de Node.js, use los botones de votos en la parte superior e inferior de esta página para enviar comentarios.</span><span class="sxs-lookup"><span data-stu-id="d119a-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="d119a-128">Si quiere que nos pongamos en contacto directamente con usted, puede incluir su dirección de correo electrónico en los comentarios.</span><span class="sxs-lookup"><span data-stu-id="d119a-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="d119a-129">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="d119a-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="d119a-130">Requisitos previos para el tutorial de Node.js</span><span class="sxs-lookup"><span data-stu-id="d119a-130">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="d119a-131">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d119a-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="d119a-132">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d119a-132">An active Azure account.</span></span> <span data-ttu-id="d119a-133">Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d119a-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="d119a-134">Como alternativa, en este tutorial puede usar el [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="d119a-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="d119a-135">[Node.js](https://nodejs.org/) versión v0.10.29 o superior</span><span class="sxs-lookup"><span data-stu-id="d119a-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="d119a-136">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d119a-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="d119a-137">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="d119a-138">Si ya tiene una cuenta que desea usar, puede ir directamente a [Configuración de la aplicación de Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="d119a-138">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="d119a-139">Si usa el Emulador de Azure Cosmos DB, siga los pasos que se indican en [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Configuración de la aplicación de Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="d119a-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="d119a-140"><a id="SetupNode"></a>Paso 2: Configuración de la aplicación de Node.js</span><span class="sxs-lookup"><span data-stu-id="d119a-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="d119a-141">Abra su terminal favorito.</span><span class="sxs-lookup"><span data-stu-id="d119a-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="d119a-142">Busque la carpeta o el directorio donde desea guardar la aplicación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="d119a-142">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="d119a-143">Cree dos archivos de JavaScript vacíos con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="d119a-143">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="d119a-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="d119a-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="d119a-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="d119a-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="d119a-146">Instale el módulo documentdb mediante npm.</span><span class="sxs-lookup"><span data-stu-id="d119a-146">Install the documentdb module via npm.</span></span> <span data-ttu-id="d119a-147">Use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d119a-147">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="d119a-148">Estupendo.</span><span class="sxs-lookup"><span data-stu-id="d119a-148">Great!</span></span> <span data-ttu-id="d119a-149">Ahora que terminamos la configuración, comencemos a escribir algo de código.</span><span class="sxs-lookup"><span data-stu-id="d119a-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="d119a-150"><a id="Config"></a>Paso 3: Configuración de las opciones de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d119a-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="d119a-151">Abra ```config.js``` en el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="d119a-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="d119a-152">Después, copie y pegue el siguiente fragmento de código y defina las propiedades ```config.endpoint``` y ```config.primaryKey``` para el identificador URI del punto de conexión de Azure Cosmos DB y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="d119a-152">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="d119a-153">Ambas opciones de configuración se encuentran en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d119a-153">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Tutorial de Node.js: captura de pantalla de Azure Portal que muestra una cuenta de Azure Cosmos DB, con el centro ACTIVO resaltado, el botón CLAVES resaltado en la hoja de la cuenta de Azure Cosmos DB y los valores de URI, CLAVE PRINCIPAL y CLAVE SECUNDARIA resaltados en la hoja Claves (base de datos de nodos)][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="d119a-155">Copie y pegue ```database id```, ```collection id``` y ```JSON documents``` en el objeto ```config``` siguiente, donde se definen las propiedades de ```config.endpoint``` y ```config.authKey```.</span><span class="sxs-lookup"><span data-stu-id="d119a-155">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="d119a-156">Si ya dispone de los datos que desea almacenar en la base de datos, puede usar la [herramienta de migración de datos](import-data.md) de Azure Cosmos DB en lugar de agregar definiciones de documento.</span><span class="sxs-lookup"><span data-stu-id="d119a-156">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="d119a-157">Las definiciones de base de datos, colección y documento actuarán como ```database id```, ```collection id``` y datos de documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-157">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="d119a-158">Por último, exporte el objeto ```config```, con el fin de que pueda hacer referencia a él en el archivo ```app.js```.</span><span class="sxs-lookup"><span data-stu-id="d119a-158">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <span data-ttu-id="d119a-159"><a id="Connect"></a>Paso 4: Conexión a una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d119a-159"><a id="Connect"></a> Step 4: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="d119a-160">Abra el archivo ```app.js``` vacío en el editor de texto.</span><span class="sxs-lookup"><span data-stu-id="d119a-160">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="d119a-161">Copie y pegue el código siguiente para importar el módulo ```documentdb``` y el módulo ```config``` que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="d119a-161">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="d119a-162">Copie y pegue el código para usar las propiedades ```config.endpoint``` y ```config.primaryKey``` que guardó anteriormente para crear un nuevo DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="d119a-162">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="d119a-163">Ahora que tiene el código necesario para inicializar el cliente de Azure Cosmos DB, se explicará cómo usar los recursos de esta solución.</span><span class="sxs-lookup"><span data-stu-id="d119a-163">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="d119a-164">Paso 5: Creación de una base de datos de nodos</span><span class="sxs-lookup"><span data-stu-id="d119a-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="d119a-165">Copie y pegue el código siguiente para definir el estado HTTP para No encontrado, la dirección URL de la base de datos y la dirección URL de la colección.</span><span class="sxs-lookup"><span data-stu-id="d119a-165">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="d119a-166">A través de estas direcciones URL el cliente de Azure Cosmos DB encontrará la base de datos y la colección adecuadas.</span><span class="sxs-lookup"><span data-stu-id="d119a-166">These urls are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="d119a-167">Para crear una [base de datos](documentdb-resources.md#databases), se puede usar la función [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d119a-167">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="d119a-168">Una base de datos es un contenedor lógico de almacenamiento de documentos particionado en recopilaciones.</span><span class="sxs-lookup"><span data-stu-id="d119a-168">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="d119a-169">Copie y pegue la función **getDatabase** para crear la base de datos nueva en el archivo app.js con el ```id``` especificado en el objeto ```config```.</span><span class="sxs-lookup"><span data-stu-id="d119a-169">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="d119a-170">La función comprobará que no existe ninguna base de datos con el mismo identificador ```FamilyRegistry``` .</span><span class="sxs-lookup"><span data-stu-id="d119a-170">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="d119a-171">Si existe, usaremos esa base de datos en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="d119a-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d119a-172">Copie y pegue el siguiente código donde defina la función **getDatabase** para agregar la función auxiliar **Salir** que imprimirá el mensaje de salida y la llamada a la función **getDatabase**.</span><span class="sxs-lookup"><span data-stu-id="d119a-172">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="d119a-173">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-173">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-174">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-174">Congratulations!</span></span> <span data-ttu-id="d119a-175">Ha creado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="d119a-176"><a id="CreateColl"></a>Paso 6: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="d119a-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="d119a-177">**CreateDocumentCollectionAsync** creará una nueva colección, que tiene implicaciones de precios.</span><span class="sxs-lookup"><span data-stu-id="d119a-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="d119a-178">Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d119a-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="d119a-179">Para crear una [colección](documentdb-resources.md#collections), puede usar la función [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d119a-179">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="d119a-180">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d119a-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="d119a-181">Copie y pegue la función **getCollection** debajo de la función **getDatabase** del archivo app.js para crear la colección nueva con el ```id``` especificado en el objeto ```config```.</span><span class="sxs-lookup"><span data-stu-id="d119a-181">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="d119a-182">Vuelva a comprobar que no existe ninguna colección con el mismo identificador ```FamilyCollection``` .</span><span class="sxs-lookup"><span data-stu-id="d119a-182">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="d119a-183">Si existe, usaremos esa colección en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="d119a-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d119a-184">Copie y pegue el código de debajo de la llamada a **getDatabase** para ejecutar la función **getCollection**.</span><span class="sxs-lookup"><span data-stu-id="d119a-184">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="d119a-185">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-185">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-186">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-186">Congratulations!</span></span> <span data-ttu-id="d119a-187">Ha creado correctamente una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="d119a-188"><a id="CreateDoc"></a>Paso 7: Creación de un documento</span><span class="sxs-lookup"><span data-stu-id="d119a-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="d119a-189">Para crear un [documento](documentdb-resources.md#documents), se puede usar la función [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="d119a-189">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="d119a-190">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="d119a-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="d119a-191">Ahora puede insertar un documento en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="d119a-192">Copie y pegue la función **getFamilyDocument** debajo de la función **getCollection** para crear los documentos que contengan los datos JSON guardados en el objeto ```config```.</span><span class="sxs-lookup"><span data-stu-id="d119a-192">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="d119a-193">Comprobaremos de nuevo que no existe ya un documento con el mismo identificador.</span><span class="sxs-lookup"><span data-stu-id="d119a-193">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d119a-194">Copie y pegue el código de debajo de la llamada a **getCollection** para ejecutar la función **getFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="d119a-194">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="d119a-195">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-195">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-196">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-196">Congratulations!</span></span> <span data-ttu-id="d119a-197">Ha creado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Tutorial de Node.js: diagrama que muestra la relación jerárquica entre la cuenta, la base de datos, la colección y los documentos (base de datos de nodos)](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="d119a-199"><a id="Query"></a>Paso 8: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d119a-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="d119a-200">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="d119a-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="d119a-201">El código de ejemplo siguiente muestra una consulta que se puede ejecutar en los documentos de la colección.</span><span class="sxs-lookup"><span data-stu-id="d119a-201">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="d119a-202">Copie y pegue la función **queryCollection** debajo de la función **getFamilyDocument** del archivo app.js.</span><span class="sxs-lookup"><span data-stu-id="d119a-202">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="d119a-203">Azure Cosmos DB admite consultas del tipo SQL tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d119a-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="d119a-204">Para más información sobre cómo crear consultas complejas, consulte [Query Playground](https://www.documentdb.com/sql/demo) y la [documentación sobre consultas](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="d119a-204">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="d119a-205">En el siguiente diagrama se muestra cómo se llama a la sintaxis de la consulta SQL de Azure Cosmos DB con la colección creada.</span><span class="sxs-lookup"><span data-stu-id="d119a-205">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![Tutorial de Node.js: diagrama que ilustra el ámbito y el significado de la consulta (base de datos de nodo).](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="d119a-207">La palabra clave [FROM](documentdb-sql-query.md#FromClause) es opcional en la consulta porque las consultas de Azure Cosmos DB ya tienen como ámbito una única colección.</span><span class="sxs-lookup"><span data-stu-id="d119a-207">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="d119a-208">Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="d119a-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="d119a-209">Azure Cosmos DB deducirá la familia, la raíz o el nombre de variable elegido y hará referencia a la colección actual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d119a-209">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="d119a-210">Copie y pegue el código de debajo de la llamada a **getFamilyDocument** para ejecutar la función **queryCollection**.</span><span class="sxs-lookup"><span data-stu-id="d119a-210">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="d119a-211">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-211">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-212">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-212">Congratulations!</span></span> <span data-ttu-id="d119a-213">Ha consultado correctamente documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="d119a-214"><a id="ReplaceDocument"></a>Paso 9: Reemplazo de un documento</span><span class="sxs-lookup"><span data-stu-id="d119a-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="d119a-215">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d119a-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="d119a-216">Copie y pegue la función **replaceFamilyDocument** debajo de la función **queryCollection** del archivo app.js.</span><span class="sxs-lookup"><span data-stu-id="d119a-216">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d119a-217">Copie y pegue el código de debajo de la llamada a **queryCollection** para ejecutar la función **replaceDocument**.</span><span class="sxs-lookup"><span data-stu-id="d119a-217">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="d119a-218">Además, agregue el código para llamar a **queryCollection** de nuevo y comprobar que el documento ha cambiado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d119a-218">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="d119a-219">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-219">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-220">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-220">Congratulations!</span></span> <span data-ttu-id="d119a-221">Ha sustituido correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="d119a-222"><a id="DeleteDocument"></a>Paso 10: Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="d119a-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="d119a-223">Azure Cosmos DB admite la eliminación de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d119a-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="d119a-224">Copie y pegue la función **deleteFamilyDocument** debajo de la función **replaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="d119a-224">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="d119a-225">Copie y pegue el código de debajo de la llamada a la segunda **queryCollection** para ejecutar la función **deleteDocument**.</span><span class="sxs-lookup"><span data-stu-id="d119a-225">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="d119a-226">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-226">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-227">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-227">Congratulations!</span></span> <span data-ttu-id="d119a-228">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="d119a-229"><a id="DeleteDatabase"></a>Paso 11: Eliminación de la base de datos de nodos</span><span class="sxs-lookup"><span data-stu-id="d119a-229"><a id="DeleteDatabase"></a>Step 11: Delete the Node database</span></span>
<span data-ttu-id="d119a-230">La eliminación de la base de datos creada quitará la base de datos y todos los recursos secundarios (colecciones, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="d119a-230">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="d119a-231">Copie y pegue la función **cleanup** debajo de la función **deleteFamilyDocument** para quitar la base de datos y todos los recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="d119a-231">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="d119a-232">Copie y pegue el código de debajo de la llamada a **deleteFamilyDocument** para ejecutar la función **cleanup**.</span><span class="sxs-lookup"><span data-stu-id="d119a-232">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="d119a-233"><a id="Run"></a>Paso 12: Ejecute íntegramente la aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="d119a-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="d119a-234">En conjunto, la secuencia para llamar a las funciones debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="d119a-234">Altogether, the sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="d119a-235">En el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="d119a-235">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="d119a-236">Ahora debería ver la salida de la aplicación GetStarted.</span><span class="sxs-lookup"><span data-stu-id="d119a-236">You should see the output of your get started app.</span></span> <span data-ttu-id="d119a-237">La salida debe coincidir con el texto del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d119a-237">The output should match the example text below.</span></span>

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
    Press any key to exit

<span data-ttu-id="d119a-238">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="d119a-238">Congratulations!</span></span> <span data-ttu-id="d119a-239">Ha completado el tutorial de Node.js y tiene su primera aplicación de consola de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d119a-239">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="d119a-240"><a id="GetSolution"></a>Obtención de la solución completa del tutorial de Node.js</span><span class="sxs-lookup"><span data-stu-id="d119a-240"><a id="GetSolution"></a>Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="d119a-241">Si no dispuso de tiempo para completar los pasos de este tutorial, o simplemente desea descargar el código, puede obtenerlo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d119a-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="d119a-242">Para ejecutar la solución GetStarted que contiene todos los ejemplos de este artículo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d119a-242">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="d119a-243">[Cuenta de Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="d119a-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="d119a-244">La solución [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d119a-244">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="d119a-245">Instale el módulo **documentdb** mediante npm.</span><span class="sxs-lookup"><span data-stu-id="d119a-245">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="d119a-246">Use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d119a-246">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="d119a-247">Después, en el archivo ```config.js``` , actualice los valores de config.endpoint y config.authKey tal como se describe en el [paso 3: Configuración de las opciones de la aplicación](#Config).</span><span class="sxs-lookup"><span data-stu-id="d119a-247">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="d119a-248">Posteriormente, en el terminal, busque el archivo ```app.js``` y ejecute el comando: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="d119a-248">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="d119a-249">Y, eso es todo, genérela y habrá terminado.</span><span class="sxs-lookup"><span data-stu-id="d119a-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d119a-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d119a-250">Next steps</span></span>
* <span data-ttu-id="d119a-251">¿Desea un ejemplo más complejo de Node.js?</span><span class="sxs-lookup"><span data-stu-id="d119a-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="d119a-252">Consulte [Creación de una aplicación web de Node.js con Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="d119a-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="d119a-253">Información acerca de cómo [supervisar una cuenta de Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="d119a-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="d119a-254">Ejecute las consultas en nuestro conjunto de datos de ejemplo en el [área de consultas](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="d119a-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="d119a-255">Obtenga más información sobre el modelo de programación en la sección sobre desarrollo de la [página de documentación de Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d119a-255">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
