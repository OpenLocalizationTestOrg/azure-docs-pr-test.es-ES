---
title: "API de DB aaaUse Azure Cosmos para MongoDB toobuild una aplicación web | Documentos de Microsoft"
description: "Tutorial de base de datos de Azure Cosmos que crea una aplicación web de base de datos en línea mediante la API de Hola para MongoDB."
keywords: ejemplos de mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="59409-104">Azure Cosmos DB: Conectar tooa MongoDB aplicaciones con .NET</span><span class="sxs-lookup"><span data-stu-id="59409-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="59409-105">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="59409-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="59409-106">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="59409-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="59409-107">Este tutorial muestra cómo toocreate una cuenta de base de datos de Azure Cosmos mediante Hola portal de Azure y cómo toocreate una base de datos y los datos de toostore de colección con Hola [API de MongoDB](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59409-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="59409-108">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="59409-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59409-109">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59409-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="59409-110">Actualización de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="59409-110">Update your connection string</span></span>
> * <span data-ttu-id="59409-111">Creación de una aplicación MongoDB en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="59409-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="59409-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="59409-112">Create a database account</span></span>

<span data-ttu-id="59409-113">Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="59409-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="59409-114">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="59409-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="59409-115">Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="59409-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="59409-116">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="59409-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="59409-117">En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="59409-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="59409-118">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="59409-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="59409-119">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="59409-119">Update your connection string</span></span>

1. <span data-ttu-id="59409-120">En el portal de Azure, en Hola Hola **base de datos de Azure Cosmos** , seleccione Hola API para la cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="59409-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="59409-121">En la barra izquierda de Hola de hoja de la cuenta de hello, haga clic en **inicio rápido**.</span><span class="sxs-lookup"><span data-stu-id="59409-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="59409-122">Elija la plataforma (*controlador .NET*, *controlador Node.js*, *MongoDB Shell*, *controlador Java*, *controlador Python*).</span><span class="sxs-lookup"><span data-stu-id="59409-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="59409-123">Si no ve el controlador o la herramienta en la lista, no se preocupe, documentamos constantemente más fragmentos de código de conexión.</span><span class="sxs-lookup"><span data-stu-id="59409-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="59409-124">Copie y pegue el fragmento de código de hello en la aplicación de MongoDB, y está listo toogo.</span><span class="sxs-lookup"><span data-stu-id="59409-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="59409-125">Configuración de la aplicación MongoDB</span><span class="sxs-lookup"><span data-stu-id="59409-125">Set up your MongoDB app</span></span>

<span data-ttu-id="59409-126">Puede usar hello [crear una aplicación web de Azure que se conecta tooMongoDB que se ejecuta en una máquina virtual](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, con una modificación mínima, el programa de instalación de tooquickly una aplicación de MongoDB (ya sea localmente o publicado tooan Azure web app) que se conecta tooan API para la cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="59409-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="59409-127">Siga el tutorial de hello, con una modificación.</span><span class="sxs-lookup"><span data-stu-id="59409-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="59409-128">Reemplace el código de hello Dal.cs a este:</span><span class="sxs-lookup"><span data-stu-id="59409-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="59409-129">Modificar Hola siguiendo las variables de hello Dal.cs archivo por la configuración de la cuenta de página de claves de Hola Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="59409-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="59409-130">¡Usar una aplicación Hola!</span><span class="sxs-lookup"><span data-stu-id="59409-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="59409-131">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="59409-131">Clean up resources</span></span>

<span data-ttu-id="59409-132">Si no va toocontinue toouse esta aplicación, utilice Hola después toodelete pasos todos los recursos creados por este tutorial Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="59409-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="59409-133">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="59409-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="59409-134">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="59409-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59409-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59409-135">Next steps</span></span>

<span data-ttu-id="59409-136">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="59409-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59409-137">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59409-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="59409-138">Actualización de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="59409-138">Update your connection string</span></span>
> * <span data-ttu-id="59409-139">Creación de una aplicación MongoDB en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="59409-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="59409-140">Puede continuar el tutorial siguiente toohello e importar su tooAzure de datos de MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59409-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="59409-141">Importación de datos de MongoDB a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59409-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

