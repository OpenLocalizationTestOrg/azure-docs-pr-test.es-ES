---
title: 'Azure Cosmos DB: Desarrollar con hello API Graph en .NET | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodevelop con la API de documentos de Azure Cosmos DB con .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB: Desarrollar con hello API Graph en .NET
Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este tutorial se muestra cómo toocreate una cuenta de base de datos de Azure Cosmos mediante Hola portal de Azure y cómo toocreate una base de datos de gráfico y el contenedor. aplicación Hello, a continuación, crea una red social simple con cuatro personas que usan hello [API Graph](graph-sdk-dotnet.md) (vista previa), a continuación, recorre y consultas gráfico de hello utilizando Gremlin.

Este tutorial trata Hola siguientes tareas:

> [!div class="checklist"]
> * Creación de una cuenta de Azure Cosmos DB 
> * Creación de un contenedor y una base de datos de grafo
> * Serializar objetos too.NET vértices y bordes
> * Incorporación de vértices y bordes
> * Gráfico de consultas hello mediante Gremlin

## <a name="graphs-in-azure-cosmos-db"></a>Grafos en Azure Cosmos DB
Puede usar base de datos de Azure Cosmos toocreate, actualización y gráficos de consultas usando hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteca. biblioteca de Hello Microsoft.Azure.Graph proporciona un método de extensión único `CreateGremlinQuery<T>` sobre hello `DocumentClient` clase consultas de Gremlin tooexecute.

Gremlin es un lenguaje de programación funcional que admite operaciones de escritura (DML) y operaciones de consulta y cruce. Trataremos algunos ejemplos en este artículo tooget el que se inició con Gremlin. Consulte las [consultas de Gremlin](gremlin-support.md) para un tutorial detallado de las funcionalidades de Gremlin disponibles en Azure Cosmos DB. 

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, puede usar hello [emulador de Azure DocumentDB](local-emulator.md) para este tutorial.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Creación de una cuenta de base de datos

Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.  

> [!TIP]
> * ¿Ya tiene una cuenta de Azure Cosmos DB? Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS)
> * ¿Ya tenía una cuenta de Azure DocumentDB? En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).  
> * Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Configuración de la solución de Visual Studio
1. Abra **Visual Studio** en el equipo.
2. En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.
3. Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **aplicación de consola (.NET Framework)**, denomine el proyecto y, a continuación, haga clic en **Aceptar**.
4. Hola **el Explorador de soluciones**, haga clic con el botón secundario en la nueva aplicación de consola, que se encuentra en la solución de Visual Studio, y, a continuación, haga clic en **administrar paquetes de NuGet...**
5. Hola **NuGet** , haga clic en **examinar**y el tipo de **Microsoft.Azure.Graphs** en el cuadro de búsqueda de Hola y Hola de comprobación **incluyen versiones preliminares**.
6. En los resultados de hello, buscar **Microsoft.Azure.Graphs** y haga clic en **instalar**.
   
   Si recibe un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**. Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.
   
    Hola `Microsoft.Azure.Graphs` biblioteca proporciona un método de extensión único `CreateGremlinQuery<T>` para ejecutar operaciones de Gremlin. Gremlin es un lenguaje de programación funcional que admite operaciones de escritura (DML) y operaciones de consulta y cruce. Trataremos algunos ejemplos en este artículo tooget el que se inició con Gremlin. El artículo sobre las [consultas de Gremlin](gremlin-support.md) ofrece un tutorial detallado de las funcionalidades de Gremlin en Azure Cosmos DB.

## <a id="add-references"></a>Conexión de la aplicación

Agregue estas dos constantes y la variable *client* en la aplicación. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
A continuación, hacer copia de head toohello [portal de Azure](https://portal.azure.com) tooretrieve la dirección URL del extremo y la clave principal. dirección URL del extremo de Hola y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación. 

Hola portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**. 

Copie Hola URI desde el portal de Hola y péguela sobre `Endpoint` en la propiedad de punto de conexión de hello anterior. A continuación, copia Hola clave principal del portal de Hola y pegarlos en hello `AuthKey` propiedad anterior. 

! [Captura de pantalla de hello portal de Azure usado por toocreate tutorial Hola una aplicación de C#. Muestra un saludo de la cuenta de base de datos de Azure Cosmos botón claves resaltado en hello navegación de la base de datos de Azure Cosmos y valores URI y la clave principal de hello resaltan en hello hoja de claves] [keys] 
 
## <a id="instantiate"></a>Crear una instancia de hello DocumentClient 
A continuación, cree una nueva instancia de hello **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Creación de una base de datos 

A continuación, cree una base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) mediante el uso de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de hello  **DocumentClient** clase a partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Creación de un grafo 

A continuación, crear un contenedor de gráficos mediante hello mediante hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método o [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de hello **DocumentClient**  clase. Una colección es un contenedor de entidades de grafo. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Serializar objetos too.NET vértices y bordes
Base de datos de Azure Cosmos usa hello [GraphSON formato](gremlin-support.md), que define un esquema JSON de vértices, bordes y propiedades. Hello Azure Cosmos DB .NET SDK incluye JSON.NET como una dependencia, y esto nos permite tooserialize/deserializar GraphSON en objetos .NET que podemos trabajar con en el código.

Como ejemplo, vamos a trabajar con una red social sencilla con cuatro personas. Veremos cómo toocreate `Person` vértices, agregar `Knows` relaciones entre ellas, a continuación, consultar y recorrer las relaciones de hello gráfico toofind "friend de confianza". 

Hola `Microsoft.Azure.Graphs.Elements` espacio de nombres proporciona `Vertex`, `Edge`, `Property` y `VertexProperty` clases para deserializar los objetos de .NET definidos por el toowell de GraphSON las respuestas.

## <a name="run-gremlin-using-creategremlinquery"></a>Ejecución de Gremlin con CreateGremlinQuery
Al igual que SQL, Gremlin admite operaciones de lectura, escritura y consulta. Por ejemplo, hello fragmento de código siguiente muestra cómo toocreate vértices, bordes, realizan algunas consultas de ejemplo con `CreateGremlinQuery<T>`y asincrónica recorrer en iteración los resultados mediante `ExecuteNextAsync` y ' HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Incorporación de vértices y bordes

Echemos un vistazo a las instrucciones de Gremlin Hola que se muestra en la sección anterior de hello más detalle. En primer lugar, creamos algunos vértices con el método `addV` de Gremlin. Por ejemplo, hello fragmento de código siguiente crea un vértice "Thomas Andersen" de tipo "Persona", con las propiedades de nombre, apellido y edad.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Luego cree algunos bordes entre estos vértices con el método `addE` de Gremlin. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Podemos usar el paso `properties` en Gremlin para actualizar un vértice existente. Se omite la consulta de Hola Hola llamada tooexecute a través de `HasMoreResults` y `ExecuteNextAsync` para el resto de Hola de ejemplos de hello.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Puede quitar bordes y vértices con el paso `drop` de Gremlin. Este es un fragmento de código que muestra cómo toodelete un vértice y un borde. Tenga en cuenta que la eliminación de un vértice realiza una eliminación en cascada de hello había asociado bordes.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Gráfico de consultas Hola

Puede realizar consultas y cruces también con Gremlin. Por ejemplo, hello siguiente fragmento de código muestra cómo toocount Hola número de vértices en el gráfico de hello:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Puede realizar filtros utilizando del Gremlin `has` y `hasLabel` los pasos y combinarlos con `and`, `or`, y `not` toobuild los filtros más complejos:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Puede proyectar ciertas propiedades de resultados de la consulta de hello mediante hello `values` paso:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Hasta ahora, solo hemos visto operadores de consulta que funcionan en cualquier base de datos. Gráficos son rápidos y eficaces para las operaciones de recorrido cuando necesite toonavigate toorelated bordes y vértices. Encontremos a todos los amigos de Thomas. Hacer esto mediante el uso del Gremlin `outE` paso toofind Hola todos los out-bordes de Thomas, a continuación, recorrer toohello vértices respecto a los bordes del Gremlin `inV` paso:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

realiza la siguiente consulta de Hello toofind de dos saltos todos "Amigos de amigos" de Thomas, mediante una llamada a `outE` y `inV` dos veces. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Puede crear consultas más complejas e implementar lógica de cruce seguro de gráfico eficaz mediante Gremlin, filtro de combinación incluido Hola de expresiones, realizar el bucle con `loop` paso y la implementación de navegación condicional mediante hello `choose` paso. Obtenga más información sobre lo que puede hacer con [Compatibilidad con Gremlin](gremlin-support.md).

Eso es todo. Ya completó el tutorial de Azure Cosmos DB 

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, utilice Hola después toodelete pasos todos los recursos creados por este tutorial Hola portal de Azure.  

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Se creó una cuenta de Azure Cosmos DB 
> * Se creó un contenedor y una base de datos de grafo
> * Objetos serializados de too.NET de vértices y bordes
> * Se agregaron vértices y bordes
> * Gráfico de hello consultado mediante Gremlin

Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo. 

> [!div class="nextstepaction"]
> [Consulta mediante Gremlin](tutorial-query-graph.md)
