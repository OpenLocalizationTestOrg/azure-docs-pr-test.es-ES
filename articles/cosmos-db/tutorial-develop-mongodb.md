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
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Azure Cosmos DB: Conectar tooa MongoDB aplicaciones con .NET

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este tutorial muestra cómo toocreate una cuenta de base de datos de Azure Cosmos mediante Hola portal de Azure y cómo toocreate una base de datos y los datos de toostore de colección con Hola [API de MongoDB](mongodb-introduction.md). 

Este tutorial trata Hola siguientes tareas:

> [!div class="checklist"]
> * Creación de una cuenta de Azure Cosmos DB 
> * Actualización de la cadena de conexión
> * Creación de una aplicación MongoDB en una máquina virtual 


## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.  

> [!TIP]
> * ¿Ya tiene una cuenta de Azure Cosmos DB? Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS)
> * ¿Ya tenía una cuenta de Azure DocumentDB? En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).  
> * Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

1. En el portal de Azure, en Hola Hola **base de datos de Azure Cosmos** , seleccione Hola API para la cuenta de MongoDB. 
2. En la barra izquierda de Hola de hoja de la cuenta de hello, haga clic en **inicio rápido**. 
3. Elija la plataforma (*controlador .NET*, *controlador Node.js*, *MongoDB Shell*, *controlador Java*, *controlador Python*). Si no ve el controlador o la herramienta en la lista, no se preocupe, documentamos constantemente más fragmentos de código de conexión. 
4. Copie y pegue el fragmento de código de hello en la aplicación de MongoDB, y está listo toogo.

## <a name="set-up-your-mongodb-app"></a>Configuración de la aplicación MongoDB

Puede usar hello [crear una aplicación web de Azure que se conecta tooMongoDB que se ejecuta en una máquina virtual](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, con una modificación mínima, el programa de instalación de tooquickly una aplicación de MongoDB (ya sea localmente o publicado tooan Azure web app) que se conecta tooan API para la cuenta de MongoDB.  

1. Siga el tutorial de hello, con una modificación.  Reemplace el código de hello Dal.cs a este:

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

2. Modificar Hola siguiendo las variables de hello Dal.cs archivo por la configuración de la cuenta de página de claves de Hola Hola portal de Azure:

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. ¡Usar una aplicación Hola!

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, utilice Hola después toodelete pasos todos los recursos creados por este tutorial Hola portal de Azure. 

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Creación de una cuenta de Azure Cosmos DB 
> * Actualización de la cadena de conexión
> * Creación de una aplicación MongoDB en una máquina virtual

Puede continuar el tutorial siguiente toohello e importar su tooAzure de datos de MongoDB Cosmos DB.  

> [!div class="nextstepaction"]
> [Importación de datos de MongoDB a Azure Cosmos DB](mongodb-migrate.md)

