---
title: "Azure Cosmos DB: Compilar una aplicación web con .NET y Hola API de documentos | Documentos de Microsoft"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consulta Hola API de documentos de base de datos de Azure Cosmos"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: Compilar una aplicación web de API de documentos con .NET y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure. A continuación, podrá compilar e implementar una aplicación de web de lista de tareas integrada en hello [API de .NET de DocumentDB](documentdb-sdk-dotnet.md), tal y como se muestra en la siguiente captura de pantalla de Hola. 

![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Requisitos previos

Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/). Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a>Agregar una colección

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Agregar datos de ejemplo

Ahora puede agregar datos tooyour nueva colección mediante el Explorador de datos.

1. En el Explorador de datos, base de datos nueva Hola aparece en panel de colecciones de Hola. Expanda hello **tareas** la base de datos, expanda hello **elementos** colección, haga clic en **documentos**y, a continuación, haga clic en **nuevos documentos**. 

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Ahora puede agregar una colección de toohello de documento con hello siguiendo la estructura.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Una vez que haya agregado Hola json toohello **documentos** , haga clic en **guardar**.

    ![Copiar datos de json y haga clic en Guardar en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Crear y guardar un documento más donde insertar un valor único para hello `id` propiedad y cambio Hola otras propiedades como considere oportuno. Los nuevos documentos pueden tener la estructura que quiera, ya que Azure Cosmos DB no impone ningún esquema en los datos.

     Ahora puede usar consultas en el Explorador de datos tooretrieve los datos. De forma predeterminada, usa el Explorador de datos `SELECT * FROM c` tooretrieve todos los documentos en la colección de hello, pero puede cambiar ese tooa diferentes [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos los documentos de hello en orden descendente en función de su marca de tiempo.
 
     También puede usar procedimientos de explorador de datos toocreate almacenado, UDF y lógica de negocios de servidor de tooperform de desencadenadores, así como el rendimiento de escala. Explorador de datos expone todo acceso a los datos de mediante programación integrada Hola disponible en las API de hello, pero proporciona un acceso sencillo tooyour datos Hola portal de Azure.

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a cambiar tooworking con el código. Vamos a clonar una aplicación de API de documentos de GitHub, establezca la cadena de conexión de Hola y ejecútelo. Podrá ver lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `CD` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. A continuación, abra el archivo de solución de hello tareas en Visual Studio. 

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Archivo de DocumentDBRepository.cs de hello abierto y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos. 

* Hola DocumentClient se inicializa en línea 73.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* Se crea una nueva base de datos en la línea 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Se crea una nueva colección en la línea 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**. Deberá usar botones de copia de hello en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en el archivo web.config de hello en el paso siguiente de saludo.

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. En Visual Studio de 2017, abra el archivo web.config de hello. 

3. Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de punto de conexión de hello en el archivo web.config. 

    `<add key="endpoint" value="FILLME" />`

4. A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo SFF hello en el archivo web.config. Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Ejecutar la aplicación web de hello
1. En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**. 

2. Hola NuGet **examinar** , escriba *DocumentDB*.

3. Desde los resultados de hello, instalar hello **Microsoft.Azure.DocumentDB** biblioteca. Esto instala el paquete de Microsoft.Azure.DocumentDB de hello, así como todas las dependencias.

4. Haga clic en CTRL + F5 aplicación hello de toorun. La aplicación se muestra en el explorador. 

5. Haga clic en **crear nuevo** Hola explorador y crear unas cuantas tareas nuevas en la aplicación de tareas pendientes.

   ![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con nuevos datos. 

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación web. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importación de datos a Azure Cosmos DB](import-data.md)


