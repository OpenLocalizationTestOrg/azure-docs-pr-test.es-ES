---
title: "Hola a aaaBuild una aplicación .NET de base de datos de Azure Cosmos con API Graph | Documentos de Microsoft"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consultar la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB: Crear una aplicación de .NET mediante Hola API Graph

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos y el gráfico (contenedor) utilizando Hola portal de Azure. A continuación, compilar y ejecutar una aplicación de consola compilada en hello [API Graph](graph-sdk-dotnet.md) (versión preliminar).  

## <a name="prerequisites"></a>Requisitos previos

Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/). Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Agregar un grafo

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una API de Graph aplicación de github, establezca la cadena de conexión de Hola y ejecútelo. Podrá ver lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. A continuación, abra Visual Studio y el archivo de solución de hello abierto. 

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Archivo de hello abra Program.cs y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos. 

* Hola DocumentClient se inicializa. En la vista previa de hello, agregamos una extensión de graph API de cliente de base de datos de Azure Cosmos Hola. Estamos trabajando en un cliente de graph independiente desacoplado de recursos y el cliente de base de datos de Azure Cosmos Hola.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Se crea una base de datos.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Se crea un grafo.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Una serie de pasos de Gremlin se ejecutan utilizando hello `CreateGremlinQuery` método.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. En Visual Studio de 2017, abra el archivo App.config de hello. 

2. Hola portal de Azure, en la cuenta de base de datos de Azure Cosmos, haga clic en **claves** Hola barra de navegación izquierda. 

    ![Ver y copiar una clave principal en el portal de Azure, en la página de claves de Hola Hola](./media/create-graph-dotnet/keys.png)

3. Copia la **URI** valor desde el portal de Hola y hacerla Hola valor de clave de punto de conexión de hello en el archivo App.config. Puede usar Hola copia botón tal como se muestra en hello anterior captura de pantalla toocopy valor de Hola.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Copia la **PRIMARY KEY** valor desde el portal de Hola y hacerla Hola valor de clave de SFF hello en el archivo App.config, a continuación, guarde los cambios. 

    `<add key="AuthKey" value="FILLME" />`

Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 

## <a name="run-hello-console-app"></a>Ejecutar la aplicación de consola de hello

1. En Visual Studio, haga doble clic en hello **GraphGetStarted** proyecto **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**. 

2. Hola NuGet **examinar** , escriba *Microsoft.Azure.Graphs* y comprobar hello **incluye versión preliminar** cuadro. 

3. Desde los resultados de hello, instalar hello **Microsoft.Azure.Graphs** biblioteca. Esto instala el paquete de biblioteca de extensión de gráfico de base de datos de Azure Cosmos de Hola y todas las dependencias.

    Si recibe un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**. Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.

4. Haga clic en CTRL + F5 aplicación hello de toorun.

   ventana de la consola de Hello muestra vértices hello y bordes añadidos toohello gráfico. Cuando finalice la secuencia de comandos de hello, presione ENTRAR dos veces tooclose Hola ventana de la consola. 

## <a name="browse-using-hello-data-explorer"></a>Examinar con hello Explorador de datos

Ahora puede volver atrás tooData Explorer Hola portal de Azure y examinar y consultar los datos de gráfico nuevo.

1. En el Explorador de datos, base de datos nueva Hola aparece en panel de gráficos de Hola. Expanda **graphdb**, **graphcollz** y, después, haga clic en **Grafo**.

2. Haga clic en hello **aplicar filtro** botón predeterminado de hello toouse consultar tooview todos los verticies de hello en el gráfico de Hola. datos de Hello generados por la aplicación de ejemplo de Hola se muestran en el panel de gráficos de Hola.

    Puede acercar la vista dentro y fuera del gráfico de hello, puede ampliar el espacio de presentación de gráfico de hello, agregar verticies adicionales y mover la superficie de presentación de verticies en Hola.

    ![Ver el gráfico de hello en el Explorador de datos en hello portal de Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos: 

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo crear un gráfico utilizando Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación. Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo. 

> [!div class="nextstepaction"]
> [Consulta mediante Gremlin](tutorial-query-graph.md)

