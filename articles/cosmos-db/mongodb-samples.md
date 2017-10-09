---
title: "aaaUse MongoDB APIs toobuild una aplicación de base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Un tutorial que crea una base de datos en línea con las API de base de datos de Azure Cosmos Hola para MongoDB."
keywords: ejemplos de mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 09be4362fe3aac02e0163325f958210be9598383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="6e13c-104">Creación de una aplicación de Azure Cosmos DB: API para MongoDB con Node.js</span><span class="sxs-lookup"><span data-stu-id="6e13c-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e13c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6e13c-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="6e13c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6e13c-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="6e13c-107">Java</span><span class="sxs-lookup"><span data-stu-id="6e13c-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="6e13c-108">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="6e13c-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="6e13c-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="6e13c-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="6e13c-110">C++</span><span class="sxs-lookup"><span data-stu-id="6e13c-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="6e13c-111">Este ejemplo muestra cómo toobuild una base de datos de Azure Cosmos: API de aplicación de consola de MongoDB mediante Node.js.</span><span class="sxs-lookup"><span data-stu-id="6e13c-111">This example shows you how toobuild an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="6e13c-112">toouse en este ejemplo, debe:</span><span class="sxs-lookup"><span data-stu-id="6e13c-112">toouse this example, you must:</span></span>

* <span data-ttu-id="6e13c-113">[Cree](create-mongodb-dotnet.md#create-account) una cuenta de Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6e13c-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="6e13c-114">Recuperar información de la [cadena de conexión](connect-mongodb-account.md) de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6e13c-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-hello-app"></a><span data-ttu-id="6e13c-115">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6e13c-115">Create hello app</span></span>

1. <span data-ttu-id="6e13c-116">Crear un *app.js* de archivos y copie y pegue el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="6e13c-116">Create a *app.js* file and copy & paste hello code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into hello families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="6e13c-117">Modificar Hola después de las variables de hello *app.js* archivo por la configuración de la cuenta (más información cómo toofind su [cadena de conexión](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="6e13c-117">Modify hello following variables in hello *app.js* file per your account settings (Learn how toofind your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="6e13c-118">Abra su terminal favorito, ejecute **npm install mongodb --save** y ejecute luego su aplicación con **node app.js**.</span><span class="sxs-lookup"><span data-stu-id="6e13c-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e13c-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e13c-119">Next steps</span></span>
* <span data-ttu-id="6e13c-120">Obtenga información acerca de cómo demasiado[usar MongoChef](mongodb-mongochef.md) con la base de datos de Azure Cosmos: API de cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6e13c-120">Learn how too[use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
