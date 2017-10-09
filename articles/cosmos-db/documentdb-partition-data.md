---
title: aaaPartitioning y ajuste de escala en la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo funciona la creación de particiones en la base de datos de Azure Cosmos, cómo tooconfigure particiones y las claves de partición, y cómo toopick Hola derecha clave de partición para la aplicación."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Creación de particiones en la base de datos de Azure Cosmos con hello API de documentos

[Base de datos de Microsoft Azure Cosmos](../cosmos-db/introduction.md) es un toohelp de servicio diseñado de base de datos distribuida, varios modelos global, obtendrá rendimiento rápido y predecible y escalabilidad sin problemas junto con la aplicación que se incremente. 

Este artículo proporciona información general sobre cómo toowork con las particiones de base de datos de Cosmos contenedores con Hola API de documentos. Consulte [la creación de particiones y el escalado horizontal](../cosmos-db/partition-data.md) para obtener una información general de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB. 

tooget a trabajar con código, descargue el proyecto Hola de [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:   

* ¿Cómo funcionan las particiones en Azure Cosmos DB?
* ¿Cómo se configuran las particiones en Azure Cosmos DB?
* ¿Cuáles son las claves de partición y cómo seleccionar clave de partición correcta de Hola para mi aplicación?

tooget a trabajar con código, descargue el proyecto Hola de [ejemplo de la controlador de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Claves de partición

En hello API de documentos, puede especificar la definición de clave de partición de hello en forma de Hola de una ruta de acceso JSON. Hello tabla siguiente muestran ejemplos de definiciones de clave de partición y valores de hello correspondientes tooeach. clave de partición de Hola se especifica como una ruta de acceso, por ejemplo, `/department` representa Hola departamento de propiedad. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Clave de partición</strong></p></td>
            <td valign="top"><p><strong>Descripción</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/department</p></td>
            <td valign="top"><p>Corresponde toohello valo doc.department donde doc es elemento Hola.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/properties/name</p></td>
            <td valign="top"><p>Corresponde toohello valo doc.properties.name donde doc es elemento hello (propiedad anidada).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/id</p></td>
            <td valign="top"><p>Corresponde toohello valo doc.id (clave de identificador y la partición se Hola misma propiedad).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/"nombre de departamento"</p></td>
            <td valign="top"><p>Corresponde toohello valo doc ["nombre de departamento"] donde doc es elemento Hola.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> sintaxis de Hola de clave de partición es similar especificación de ruta de acceso de toohello para indizar rutas de acceso de directiva con la diferencia clave Hola que Hola ruta de acceso correspondiente propiedad toohello en lugar del valor de hello, es decir, no es ningún carácter comodín al final de Hola. ¿Por ejemplo, especificaría /department/? Hola tooindex valores en departamento, pero especifique /department como definición de clave de partición de Hola. clave de partición de Hello está indexada de forma implícita y no se puede excluir de la indización mediante invalidaciones de directiva de indización.
> 
> 

Echemos un vistazo a la elección de Hola de clave de partición afecta al rendimiento de hello de la aplicación.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Trabajar con hello Azure Cosmos DB SDK
A partir de la [versión de la API de REST de 16-12-2015](/rest/api/documentdb/), Azure Cosmos DB admite la creación automática de particiones. Admite más reciente en uno de Hola o en contenedores de orden toocreate particionado, debe descargar las versiones del SDK 1.6.0 plataformas SDK (. NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Creación de contenedores
Hello en el ejemplo siguiente se muestra un toocreate de fragmento de código de .NET un contenedor toostore dispositivo los datos de telemetría de 20.000 unidades de solicitud por segundo de rendimiento. Hola SDK establece el valor de OfferThroughput de hello (que a su vez establece hello `x-ms-offer-throughput` encabezado de solicitud de hello API de REST). A continuación establecemos hello `/deviceId` como clave de partición de Hola. opción de Hola de clave de partición se guarda junto con el resto de Hola de hello metadatos del contenedor como nombre y la directiva de indexación.

Para este ejemplo, se seleccionarán `deviceId` puesto que sabemos que (a) puesto que hay un gran número de dispositivos, escrituras se pueden distribuir en particiones uniformemente y lo que nos tooscale Hola tooingest grandes volúmenes de datos de base de datos y (b) muchas de las solicitudes de hello como obtención de lectura más reciente de Hola para un dispositivo son tooa ámbito único deviceId y pueden obtenerse de una sola partición.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Este método realiza una API de REST llamada tooCosmos base de datos y servicio Hola proporcionará un número de particiones según rendimiento solicitado Hola. Puede cambiar el rendimiento de un contenedor de hello según sus necesidades de rendimiento evolucionan. 

### <a name="reading-and-writing-items"></a>Lectura y escritura de elementos
Ahora, insertemos los datos en Cosmos DB. Esta es una clase de ejemplo que contiene una lectura de dispositivo y un tooinsert de tooCreateDocumentAsync de llamada a un nuevo dispositivo de lectura en un contenedor. Este es un ejemplo que aprovecha Hola API de documentos:

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

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
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

Vamos a leer el elemento Hola por su clave de partición y el Id., actualizar y como paso final, elimínela identificador y la clave de partición. Tenga en cuenta que las lecturas Hola incluyen un valor de PartitionKey (toohello correspondiente `x-ms-documentdb-partitionkey` encabezado de solicitud de hello API de REST).

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a>Consulta de contenedores con particiones
Al consultar los datos en contenedores con particiones, base de datos de Cosmos automáticamente las rutas Hola particiones toohello de consulta correspondiente a los valores de clave de partición de toohello especificados en el filtro de hello (si hay alguno). Por ejemplo, esta consulta es la clave de partición Hola de contenedor de partición de hello del toojust enrutado "XMS-0001".

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

Cosmos DB admite las [funciones de agregado](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` y `AVG` en contenedores con particiones mediante SQL a partir del SDK 1.12.0, y versiones posteriores. Las consultas deben incluir un operador agregado único y deben incluir un valor único en la proyección de Hola.

### <a name="parallel-query-execution"></a>Ejecución de consultas en paralelo
Hola Cosmos DB SDK 1.9.0 y versiones posteriores admite opciones de ejecución de consultas en paralelo, lo que permite una latencia baja tooperform consultas en colecciones con particiones, incluso cuando los necesitan tootouch un gran número de particiones. Por ejemplo, hello después de consulta es toorun configurado en paralelo en particiones.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Puede administrar la ejecución de consultas en paralelo ajustando Hola parámetros siguientes:

* Estableciendo `MaxDegreeOfParallelism`, puede controlar el grado de Hola de paralelismo, es decir, Hola número máximo de particiones del contenedor de las toohello de conexiones de red simultáneas. Si se establece demasiado-1, se administra el grado de paralelismo Hola Hola SDK. Si hello `MaxDegreeOfParallelism` no se ha especificado o establecer too0, que es el valor predeterminado de hello, habrá particiones del contenedor toohello de conexión de red único.
* Al establecer `MaxBufferedItemCount`, puede compensar el uso de memoria por parte del cliente y la latencia en las consultas. Si omite este parámetro o se establece demasiado-1, número de Hola de elementos almacenados en búfer durante la ejecución de consultas en paralelo es administrado por hello SDK.

Dados Hola mismo estado de recopilación de hello, una consulta en paralelo devolverá resultados Hola mismo pedido como en ejecución en serie. Al realizar una consulta entre particiones que incluye la ordenación (ORDER BY o superior), problemas de SDK de base de datos de Azure Cosmos Hola Hola consulta en paralelo a través de las particiones y combinaciones resultados parcialmente ordenados en tooproduce de lado cliente hello resultados ordenados globalmente.

### <a name="executing-stored-procedures"></a>Ejecución de procedimientos almacenados
También puede ejecutar transacciones atómicas con documentos con Hola mismo Id. de dispositivo, por ejemplo, si desea mantener agregados u Hola estado más reciente de un dispositivo en un único elemento. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
En la siguiente sección hello, veremos cómo puede trasladar toopartitioned contenedores de contenedores de partición única.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, se proporciona información general sobre cómo toowork con las particiones de base de datos de Azure Cosmos contenedores con Hola API de documentos. Consulte también [la creación de particiones y el escalado horizontal](../cosmos-db/partition-data.md) para obtener una información general de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB. 

* Realice pruebas de escala y de rendimiento con Azure Cosmos DB. Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md) para ver ejemplos.
* Comenzar a codificar con hello [SDK](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/)
* Información sobre el [procesamiento aprovisionado en Azure Cosmos DB](request-units.md)

