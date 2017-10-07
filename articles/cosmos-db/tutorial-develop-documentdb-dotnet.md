---
title: 'Azure Cosmos DB: Desarrollar con hello API de documentos en .NET | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodevelop con la API de documentos de Azure Cosmos DB con .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: Desarrollar con hello API de documentos en .NET

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este tutorial muestra cómo toocreate una cuenta de base de datos de Azure Cosmos mediante Hola portal de Azure y, a continuación, crear una base de datos de documento y una colección con un [clave de partición](documentdb-partition-data.md#partition-keys) con hello [API de .NET de DocumentDB](documentdb-introduction.md). Mediante la definición de una clave de partición cuando se crea una colección, la aplicación está preparada tooscale sin esfuerzo a medida que aumentan los datos. 

Tareas de continuación Hola tutorial abarca mediante el uso de hello [API de .NET de DocumentDB](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Creación de una cuenta de Azure Cosmos DB
> * Creación de una base de datos y colección con una clave de partición
> * Creación de documentos JSON
> * Actualización de un documento
> * Consulta de colecciones con particiones
> * Ejecución de procedimientos almacenados
> * Eliminar un documento
> * Eliminación de una base de datos

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial si desea que toouse un entorno local que emula el servicio de Azure DocumentDB Hola para fines de desarrollo.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-an-azure-cosmos-db-account"></a>Creación de una cuenta de Azure Cosmos DB

Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.

> [!TIP]
> * ¿Ya tiene una cuenta de Azure Cosmos DB? Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS)
> * ¿Ya tenía una cuenta de Azure DocumentDB? En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).  
> * Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Configuración de la solución de Visual Studio
1. Abra **Visual Studio** en el equipo.
2. En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.
3. Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **aplicación de consola (.NET Framework)**, denomine el proyecto y, a continuación, haga clic en **Aceptar**.
   ![Captura de pantalla de ventana nuevo proyecto de hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. Hola **el Explorador de soluciones**, haga clic con el botón secundario en la nueva aplicación de consola, que se encuentra en la solución de Visual Studio, y, a continuación, haga clic en **administrar paquetes de NuGet...**
    
    ![Captura de pantalla de hello derecha menú Clicked Hola proyecto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. Hola **NuGet** , haga clic en **examinar**y el tipo de **documentdb** en el cuadro de búsqueda de Hola.
<!---stopped here--->
6. En los resultados de hello, buscar **Microsoft.Azure.DocumentDB** y haga clic en **instalar**.
   Id. de paquete de Hola para hello biblioteca de cliente de base de datos de Azure Cosmos es [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Captura de pantalla de hello NuGet menú para buscar el SDK de cliente de base de datos de Azure Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Si recibe un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**. Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.

## <a id="Connect"></a>Agregar referencias tooyour proyecto
Hola restantes pasos de este tutorial proporcione Hola API de documentos código fragmentos de código toocreate y actualización de base de datos de Azure Cosmos recursos necesarios en el proyecto.

En primer lugar, agregue estas aplicaciones de tooyour de referencias.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Conexión de la aplicación

A continuación, agregue estas dos constantes y la variable *client* en la aplicación.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

A continuación, hacer copia de head toohello [portal de Azure](https://portal.azure.com) tooretrieve la dirección URL del extremo y la clave principal. dirección URL del extremo de Hola y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.

Hola portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.

Copie Hola URI desde el portal de Hola y péguela sobre `<your endpoint URL>` en el archivo program.cs de Hola. A continuación, copiar Hola clave principal del portal de Hola y péguela sobre `<your primary key>`. Estar seguro de hello tooremove `<` y `>` de sus valores.

![Captura de pantalla de hello portal de Azure usa Hola NoSQL tutorial toocreate una aplicación de consola de C#. Muestra una cuenta de base de datos de Azure Cosmos con hello claves resaltadas en la hoja de la cuenta de base de datos de Azure Cosmos de hello y Hola URI y valores de clave principal resaltados en la hoja de claves de Hola](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Crear una instancia de hello DocumentClient

Ahora, cree una nueva instancia de hello **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Creación de una base de datos

A continuación, cree una base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) mediante el uso de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de hello  **DocumentClient** clase a partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md). Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Decisión sobre una clave de partición 

Las colecciones son contenedores para almacenar documentos. Son recursos lógicos y pueden [abarcar una o varias particiones físicas](partition-data.md). A [clave de partición](documentdb-partition-data.md) es una propiedad (o ruta de acceso) dentro de los documentos que está toodistribute usa los datos entre los servidores de Hola o particiones. Hola a todos los documentos con hello misma clave de partición se almacenan en misma partición. 

Determinar una clave de partición es una decisión importante toomake antes de crear una colección. Las claves de partición son una propiedad (o la ruta de acceso) en los documentos que pueden ser utilizado por la base de datos de Azure Cosmos toodistribute los datos entre varios servidores o las particiones. COSMOS DB aplica un algoritmo hash de valor de clave de partición de Hola y utiliza la partición de Hola de toodetermine de resultado de hello aplica un algoritmo hash en qué documento de hello toostore. Hola a todos los documentos con hello misma clave de partición se almacenan en misma partición y las claves de partición no se puede cambiar una vez que se crea una colección. 

Para este tutorial, vamos clave de partición de hello tooset demasiado`/deviceId` así que Hola a todos los datos de Hola para un único dispositivo se almacena en una sola partición. Desea toochoose una clave de partición que tiene un gran número de valores, cada uno de los cuales se usan en sobre hello tooensure de frecuencia mismo Cosmos DB puede equilibrar la carga que los datos aumenta y lograr un rendimiento total de colección de Hola Hola. 

¿Para obtener más información acerca de las particiones, vea [cómo toopartition y la escala en la base de datos de Azure Cosmos?](partition-data.md) 

## <a id="CreateColl"></a>Creación de una colección 

Ahora que sabemos que la clave de partición, `/deviceId`, permite crear un [colección](documentdb-resources.md#collections) mediante el uso de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método o [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de hello **DocumentClient** clase. Una colección es un contenedor de documentos JSON y cualquier lógica de aplicación JavaScript asociada. 

> [!WARNING]
> Crear una colección tiene precios implicaciones, tal y como está reservando para hello toocommunicate de aplicación con la base de datos de Azure Cosmos rendimiento. Para más detalles, visite la [página sobre precios](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Esto hace que la método una API de REST llamada tooAzure DB Cosmos y Hola un número de particiones según rendimiento solicitado Hola de disposiciones de servicio. Puede cambiar el rendimiento de una colección Hola según sus necesidades de rendimiento evolucionar utilizando Hola SDK o hello [portal de Azure](set-throughput.md).

## <a id="CreateDoc"></a>Creación de documentos JSON
Vamos a insertar algunos documentos JSON en Azure Cosmos DB. A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de hello **DocumentClient** clase. Los documentos son contenido JSON definido por el usuario (arbitrario). Esta clase de ejemplo contiene una lectura de dispositivo y un tooinsert de tooCreateDocumentAsync de llamada a un nuevo dispositivo de lectura en una colección.

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a>Lectura de datos

Vamos a leer documento Hola por su clave de partición y el identificador mediante el método ReadDocumentAsync de hello. Tenga en cuenta que las lecturas Hola incluyen un valor de PartitionKey (toohello correspondiente `x-ms-documentdb-partitionkey` encabezado de solicitud de hello API de REST).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Actualización de datos

Ahora vamos a actualizar algunos datos utilizando el método de hello ReplaceDocumentAsync.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Eliminación de datos

Ahora permite eliminar un documento por clave de partición y el identificador mediante el método de hello DeleteDocumentAsync.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Consulta de colecciones con particiones

Al consultar datos en colecciones con particiones, la base de datos de Azure Cosmos automáticamente las rutas Hola particiones toohello de consulta correspondiente a los valores de clave de partición de toohello especificados en el filtro de hello (si hay alguno). Por ejemplo, esta consulta es la clave de partición Hola de contenedor de partición de hello del toojust enrutado "XMS-0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Hola siguiente consulta no tiene un filtro en la clave de partición de hello (DeviceId) y es en abanico particiones tooall donde se ejecuta en el índice de la partición de Hola. Tenga en cuenta que tener hello toospecify EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` Hola API de REST) toohave Hola SDK tooexecute una consulta en particiones.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a>Ejecución de consultas en paralelo
Hola SDK de documentos de base de datos de Azure Cosmos 1.9.0 y versiones posteriores admite opciones de ejecución de consultas en paralelo, lo que permite una latencia baja tooperform consultas en colecciones con particiones, incluso cuando los necesitan tootouch un gran número de particiones. Por ejemplo, hello después de consulta es toorun configurado en paralelo en particiones.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Puede administrar la ejecución de consultas en paralelo ajustando Hola parámetros siguientes:

* Estableciendo `MaxDegreeOfParallelism`, puede controlar el grado de Hola de paralelismo es decir, Hola número máximo de particiones de la colección de las toohello de conexiones de red simultáneas. Si se establece demasiado-1, se administra el grado de paralelismo Hola Hola SDK. Si hello `MaxDegreeOfParallelism` no se ha especificado o establecer too0, que es el valor predeterminado de hello, habrá particiones de la colección toohello de conexión de red único.
* Al establecer `MaxBufferedItemCount`, puede compensar el uso de memoria por parte del cliente y la latencia en las consultas. Si omite este parámetro o se establece demasiado-1, número de Hola de elementos almacenados en búfer durante la ejecución de consultas en paralelo es administrado por hello SDK.

Dados Hola mismo estado de recopilación de hello, una consulta en paralelo devolverá resultados Hola mismo pedido como en ejecución en serie. Al realizar una consulta entre particiones que incluye la ordenación (ORDER BY o superior), hello DocumentDB SDK emite consultas hello en paralelo en particiones y combina los resultados ordenados parcialmente en tooproduce de lado cliente hello resultados ordenados globalmente.

## <a name="execute-stored-procedures"></a>Ejecución de procedimientos almacenados
Por último, puede ejecutar transacciones atómicas con documentos con Hola mismo Id. de dispositivo, por ejemplo, si desea mantener agregados u Hola estado más reciente de un dispositivo en un único documento agregando Hola siguiendo el proyecto de código tooyour.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

Eso es todo. esos son componentes principales de Hola de una aplicación de base de datos de Azure Cosmos que utiliza una distribución de datos de escala de tooefficiently clave de partición en particiones.  

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial Hola portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en hello único nombre de recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello: 

> [!div class="checklist"]
> * Se creó una cuenta de Azure Cosmos DB
> * Se creó una base de datos y una colección con una clave de partición
> * Se crearon documentos JSON
> * Se actualizó un documento
> * Se consultaron colecciones con particiones
> * Se ejecutó un procedimiento almacenado
> * Se eliminó un documento
> * Se eliminó una base de datos

Ahora puede continuar el tutorial siguiente toohello e importar cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importación de datos a Azure Cosmos DB](import-data.md)
