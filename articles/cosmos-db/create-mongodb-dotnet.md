---
title: "Azure Cosmos DB: Compilar una aplicación web con .NET y Hola MongoDB API | Documentos de Microsoft"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consulta hello Azure Cosmos DB MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: Compilar una aplicación web de API de MongoDB con .NET y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure. A continuación, podrá compilar e implementar una aplicación de web de lista de tareas integrada en hello [controlador MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Requisitos previos

Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/). Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una API de MongoDB aplicación de github, establezca la cadena de conexión de Hola y ejecútelo. Podrá ver lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. A continuación, abra el archivo de solución de hello en Visual Studio. 

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Abra hello **Dal.cs** archivo bajo hello **DAL** directorio y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos. 

* Inicializar hello Mongo cliente.

    ```cs
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
    ```

* Recuperar la base de datos de Hola y colección de Hola.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Recupere todos los documentos.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **cadena de conexión**y, a continuación, haga clic en **claves de lectura y escritura**. Deberá usar botones de copia de hello en hello derecha de Hola Hola de toocopy pantalla nombre de usuario, la contraseña y el Host en el archivo Dal.cs de hello en el paso siguiente de Hola.

2. Abra hello **Dal.cs** archivo Hola **DAL** directory. 

3. Copia la **nombre de usuario** valor desde portal hello (mediante el botón Copiar de hello) y hacerla Hola valo hello **nombre de usuario** en su **Dal.cs** archivo. 

4. A continuación, copie su **host** valor desde el portal de Hola y hacerla Hola valo hello **host** en su **Dal.cs** archivo. 

5. Por último, copie su **contraseña** valor desde el portal de Hola y hacerla Hola valo hello **contraseña** en su **Dal.cs** archivo. 

Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 
    
## <a name="run-hello-web-app"></a>Ejecutar la aplicación web de hello

1. En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**. 

2. Hola NuGet **examinar** , escriba *MongoDB.Driver*.

3. Desde los resultados de hello, instalar hello **MongoDB.Driver** biblioteca. Esto instala el paquete de MongoDB.Driver de hello, así como todas las dependencias.

4. Haga clic en CTRL + F5 aplicación hello de toorun. La aplicación se muestra en el explorador. 

5. Haga clic en **crear** Hola explorador y crear unas nuevas tareas en la aplicación de la lista de tareas.

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación web con Hola API para MongoDB. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importar datos en la base de datos de Azure Cosmos para hello API de MongoDB](mongodb-migrate.md)

