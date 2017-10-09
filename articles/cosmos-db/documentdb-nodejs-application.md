---
title: "una aplicación web de Node.js para la base de datos de Azure Cosmos aaaBuild | Documentos de Microsoft"
description: "Este tutorial Node.js explora cómo toouse datos de base de datos de Microsoft Azure Cosmos toostore y acceso desde una aplicación web de Node.js Express se hospeda en sitios Web de Azure."
keywords: "Desarrollo de aplicaciones, tutorial de base de datos, información sobre node.js, tutorial de node.js"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="2f6cd-104"><a name="_Toc395783175"></a>Creación de una aplicación web de Node.js con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f6cd-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f6cd-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2f6cd-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="2f6cd-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="2f6cd-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="2f6cd-107">Java</span><span class="sxs-lookup"><span data-stu-id="2f6cd-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="2f6cd-108">Python</span><span class="sxs-lookup"><span data-stu-id="2f6cd-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="2f6cd-109">Este tutorial Node.js muestra cómo se hospedan hello documentos API toostore y datos de acceso desde una aplicación de Node.js Express y toouse base de datos de Azure Cosmos en sitios Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="2f6cd-110">Compile una aplicación de administración de tareas basadas en web sencilla, una aplicación ToDo, que permite crear, recuperar y completar tareas.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="2f6cd-111">tareas de Hola se almacenan como documentos JSON en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="2f6cd-112">Este tutorial le guía a través de la creación de hello y la implementación de la aplicación hello y explica lo que sucede en cada fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Captura de pantalla de aplicación de mi lista de tareas creada en este tutorial Node.js Hola](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="2f6cd-114">¿No tener tiempo toocomplete Hola tutorial y simplemente desea solución completa de hello tooget?</span><span class="sxs-lookup"><span data-stu-id="2f6cd-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="2f6cd-115">No hay problema, puede obtener la solución de ejemplo completo de Hola desde [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2f6cd-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="2f6cd-116">Tan solo los lee hello [Léame](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) archivo para obtener instrucciones sobre cómo toorun Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="2f6cd-117"><a name="_Toc395783176"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2f6cd-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="2f6cd-118">En este tutorial de Node.js se presupone que tiene experiencia previa con el uso de Node.js y los sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="2f6cd-119">Antes de seguir las instrucciones de hello en este artículo, debe asegurarse de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="2f6cd-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-120">An active Azure account.</span></span> <span data-ttu-id="2f6cd-121">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2f6cd-122">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="2f6cd-123">OR</span><span class="sxs-lookup"><span data-stu-id="2f6cd-123">OR</span></span>

   <span data-ttu-id="2f6cd-124">Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md) (sólo Windows).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="2f6cd-125">[Node.js][Node.js] versión v0.10.29 o superior.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="2f6cd-126">[Express Generator](http://www.expressjs.com/starter/generator.html) (puede instalarlo mediante `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="2f6cd-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="2f6cd-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="2f6cd-127">[Git][Git].</span></span>

## <span data-ttu-id="2f6cd-128"><a name="_Toc395637761"></a>Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f6cd-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="2f6cd-129">Para comenzar, creemos una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="2f6cd-130">Si ya tiene una cuenta o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[paso 2: crear una nueva aplicación de Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="2f6cd-131"><a name="_Toc395783178"></a>Paso 2: Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="2f6cd-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="2f6cd-132">Ahora vamos a aprender toocreate un proyecto básico de Hello World Node.js con hello [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="2f6cd-133">Abra su terminal favorito, como símbolo de hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="2f6cd-134">Navegue directorio toohello en el que desea nueva aplicación de toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="2f6cd-135">Usar Hola generador express toogenerate llama a una nueva aplicación **tareas**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="2f6cd-136">Abra el nuevo directorio **todo** e instale las dependencias.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="2f6cd-137">Ejecute la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="2f6cd-138">Puede ver la nueva aplicación llevando el explorador demasiado[http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Obtenga información acerca de Node.js - captura de pantalla de hello aplicación Hola a todos en una ventana del explorador](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="2f6cd-140">A continuación, toostop Hola aplicación, presione CTRL+C en la ventana de terminal de hello y, a continuación, haga clic en **y** proceso por lotes de tooterminate Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="2f6cd-141"><a name="_Toc395783179"></a>Paso 3: Instalación de módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="2f6cd-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="2f6cd-142">Hola **package.json** archivo es uno de los archivos de hello creados en hello raíz del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="2f6cd-143">Este archivo contiene una lista de módulos adicionales necesarios para una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="2f6cd-144">Más adelante, cuando se implementa esta tooAzure aplicación sitios Web, este archivo es utilizado toodetermine qué toobe de necesidad de módulos instalados en Azure toosupport la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="2f6cd-145">Se sigue necesitan tooinstall dos más paquetes para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="2f6cd-146">Nuevo en hello terminal, instalar hello **async** módulo a través de npm.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="2f6cd-147">Instalar hello **documentdb** módulo a través de npm.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="2f6cd-148">Se trata de módulo de Hola donde ocurre mágico de base de datos de Azure Cosmos Hola todos los.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="2f6cd-149">Una comprobación rápida de hello **package.json** archivo de aplicación hello debe mostrar hello módulos adicionales.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="2f6cd-150">Este archivo se indican qué toodownload paquetes de Azure e instalar cuando se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="2f6cd-151">Debe parecerse al siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-151">It should resemble hello example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="2f6cd-152">Esto indica a Node (y a Azure más tarde) que la aplicación depende de estos módulos adicionales.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="2f6cd-153"><a name="_Toc395783180"></a>Paso 4: Usar el servicio de base de datos de Azure Cosmos hello en una aplicación de nodo</span><span class="sxs-lookup"><span data-stu-id="2f6cd-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="2f6cd-154">Que encarga de todo el programa de instalación inicial de Hola y la configuración, ahora vamos a get hacia abajo toowhy estamos aquí y se toowrite algunos programe con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="2f6cd-155">Crear modelo Hola</span><span class="sxs-lookup"><span data-stu-id="2f6cd-155">Create hello model</span></span>
1. <span data-ttu-id="2f6cd-156">En el directorio del proyecto hello, cree un directorio denominado **modelos** Hola mismo directorio que el archivo de hello package.json.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="2f6cd-157">Hola **modelos** directorio, cree un nuevo archivo denominado **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="2f6cd-158">Este archivo contendrá el modelo de Hola para las tareas de hello creadas por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="2f6cd-159">En Hola mismo **modelos** directorio, cree otro nuevo archivo denominado **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="2f6cd-160">Este archivo contendrá código útil y reutilizable que se utilizará en toda nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="2f6cd-161">Código de copia Hola siguiente en demasiado**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="2f6cd-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="2f6cd-162">Guarde y cierre hello **docdbUtils.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="2f6cd-163">En principio Hola de hello **taskDao.js** , agregue Hola después Hola de código tooreference **DocumentDBClient** hello y **docdbUtils.js** hemos creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="2f6cd-164">A continuación, agregará código toodefine y exportar el objeto de tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="2f6cd-165">Esto es responsable de inicializar el objeto de tarea y la configuración de hello base de datos y la colección de documentos que se usará.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="2f6cd-166">A continuación, agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="2f6cd-167">Guarde y cierre hello **taskDao.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="2f6cd-168">Crear controlador Hola</span><span class="sxs-lookup"><span data-stu-id="2f6cd-168">Create hello controller</span></span>
1. <span data-ttu-id="2f6cd-169">Hola **rutas** directorio del proyecto, cree un nuevo archivo denominado **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="2f6cd-170">Agregar Hola sigue código demasiado**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="2f6cd-171">Esto carga los módulos de hello DocumentDBClient y asincrónicas, que son usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="2f6cd-172">Esto también define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="2f6cd-173">Continúe agregando toohello **tasklist.js** archivo mediante la adición de métodos de hello usa demasiado**showTasks, addTask**, y **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="2f6cd-174">Guarde y cierre hello **tasklist.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="2f6cd-175">Agregar config.js</span><span class="sxs-lookup"><span data-stu-id="2f6cd-175">Add config.js</span></span>
1. <span data-ttu-id="2f6cd-176">En el directorio del proyecto, cree un nuevo archivo con el nombre **config.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="2f6cd-177">Agregue la Hola siguiente demasiado**config.js**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="2f6cd-178">Así se definen las opciones de configuración y los valores necesarios para nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="2f6cd-179">Hola **config.js** de archivos, valores de hello de actualización de HOST y AUTH_KEY con valores de hello que se encuentran en la hoja de claves de saludo de la cuenta de base de datos de Azure Cosmos en hello [portal de Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="2f6cd-180">Guarde y cierre hello **config.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="2f6cd-181">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="2f6cd-181">Modify app.js</span></span>
1. <span data-ttu-id="2f6cd-182">En el directorio del proyecto hello, abra hello **app.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="2f6cd-183">Este archivo se creó anteriormente cuando se creó la aplicación web de hello Express.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="2f6cd-184">Agregar Hola después de la parte superior de toohello de código de **app.js**</span><span class="sxs-lookup"><span data-stu-id="2f6cd-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="2f6cd-185">Este código define toobe de archivo de configuración de hello usa y continúa tooread valores fuera de este archivo en algunas de las variables que se usará pronto.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="2f6cd-186">Reemplace Hola después de dos líneas en **app.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="2f6cd-187">con hello siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-187">with hello following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="2f6cd-188">Estas líneas definen una nueva instancia de nuestro **TaskDao** objeto, con un tooAzure de conexión nueva base de datos de Cosmos (utilizando los valores de hello leído en hello **config.js**), inicializar el objeto de tarea de hello y, a continuación, enlazar las acciones de formulario toomethods en nuestra **TaskList** controlador.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="2f6cd-189">Por último, guarde y cierre hello **app.js** archivo, casi acabamos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="2f6cd-190"><a name="_Toc395783181"></a>Paso 5: Creación de una interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="2f6cd-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="2f6cd-191">Ahora vamos a activar la interfaz de usuario de atención toobuilding Hola para un usuario pueda interactuar realmente con nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="2f6cd-192">Hola aplicación Express creamos usa **Jade** como motor de vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="2f6cd-193">Para obtener más información sobre Jade consulte demasiado[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="2f6cd-194">Hola **layout.jade** archivo Hola **vistas** directory se utiliza como plantilla global para otro **.jade** archivos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="2f6cd-195">En este paso, modificará toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign un sitio Web de aspecto "nice".</span><span class="sxs-lookup"><span data-stu-id="2f6cd-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="2f6cd-196">Abra hello **layout.jade** archivo se encuentra en hello **vistas** carpeta y reemplazar contenido Hola con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="2f6cd-197">Esto indica eficazmente hello **Jade** motor toorender algo de HTML para nuestra aplicación y crea un **bloque** llama **contenido** donde poder proporcionar el diseño de Hola para nuestro contenido páginas.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="2f6cd-198">Guarde y cierre este archivo **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="2f6cd-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="2f6cd-199">Ahora, abra hello **index.jade** archivo, la vista de Hola que se usará en nuestra aplicación y reemplace el contenido de Hola de archivo hello con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="2f6cd-200">Esto amplía el diseño y proporciona contenido de hello **contenido** marcador de posición que hemos visto en hello **layout.jade** versiones anteriores de archivos.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="2f6cd-201">En este diseño hemos creado dos formularios HTML.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="2f6cd-202">primera forma de Hello contiene una tabla de nuestros datos y un botón que nos permite tooupdate elementos publicando demasiado**/completetask** método de nuestro controlador.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="2f6cd-203">segunda forma de Hello contiene dos campos de entrada y un botón que nos permite toocreate un nuevo elemento publicando demasiado**/addtask** método de nuestro controlador.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="2f6cd-204">Debe ser todo lo que necesitamos para nuestro toowork de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="2f6cd-205"><a name="_Toc395783181"></a>Paso 6: Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="2f6cd-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="2f6cd-206">aplicación de hello tootest en el equipo local, ejecute `npm start` en Hola terminal toostart la aplicación, a continuación, actualice su [http://localhost:3000](http://localhost:3000) página del explorador.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="2f6cd-207">página de Hello debe ser ahora similar a la imagen de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="2f6cd-207">hello page should now look like hello image below:</span></span>
   
    ![Captura de pantalla de hello aplicación MyTodo lista en una ventana del explorador](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="2f6cd-209">Si recibe un error acerca de la sangría de hello en archivos de layout.jade de Hola o hello index.jade, asegúrese de que las dos primeras líneas de hello en los dos archivos está justificado a la izquierda, sin espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="2f6cd-210">Si hay espacios antes que dos primeras las hello, quitarlos, guardar ambos archivos, a continuación, actualice la ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="2f6cd-211">Hola elemento, el nombre del elemento y la categoría campos tooenter una nueva tarea y, a continuación, haga clic en **Agregar elemento**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="2f6cd-212">Esto crea un documento en Azure Cosmos DB con esas propiedades.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="2f6cd-213">página de Hello debe actualizar hello toodisplay recién creado del elemento de lista de tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Captura de pantalla de la aplicación hello con un nuevo elemento en la lista de tareas de Hola](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="2f6cd-215">toocomplete una tarea, solo tiene que activar casilla hello en la columna completa de hello y, a continuación, haga clic en **actualizar tareas**.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="2f6cd-216">Este documento de hello las actualizaciones que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="2f6cd-217">aplicación de hello toostop, presione CTRL+C en la ventana de terminal de hello y, a continuación, haga clic en **Y** proceso por lotes de tooterminate Hola.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="2f6cd-218"><a name="_Toc395783182"></a>Paso 7: Implementar el proyecto de desarrollo aplicación tooAzure sitios Web</span><span class="sxs-lookup"><span data-stu-id="2f6cd-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="2f6cd-219">Si todavía no lo ha hecho, habilite un repositorio para el sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="2f6cd-220">Encontrará instrucciones sobre cómo toodo esto en hello [tooAzure servicio de aplicaciones de la implementación de Git Local](../app-service-web/app-service-deploy-local-git.md) tema.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="2f6cd-221">Agregue el sitio web de Azure como un git remoto.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="2f6cd-222">Implementar mediante la inserción de toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="2f6cd-223">En pocos segundos, git terminará de publicar su aplicación web y ejecutará un explorador donde podrá ver su útil trabajo ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="2f6cd-224">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2f6cd-224">Congratulations!</span></span> <span data-ttu-id="2f6cd-225">Acaba de compilar la primera Node.js Express aplicación Web con la base de datos de Azure Cosmos y haberlo publicado tooAzure sitios Web.</span><span class="sxs-lookup"><span data-stu-id="2f6cd-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="2f6cd-226">Si desea que toodownload o consulte la aplicación de referencia completa de toohello para este tutorial, se puede descargar desde [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2f6cd-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="2f6cd-227"><a name="_Toc395637775"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f6cd-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="2f6cd-228">¿Desea tooperform escala y rendimiento de pruebas con la base de datos de Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="2f6cd-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="2f6cd-229">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="2f6cd-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="2f6cd-230">Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="2f6cd-231">Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2f6cd-232">Explorar hello [documentación de la base de datos de Azure Cosmos](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2f6cd-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

