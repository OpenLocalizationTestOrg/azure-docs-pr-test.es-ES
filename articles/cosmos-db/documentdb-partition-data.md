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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="4f196-103">Creación de particiones en la base de datos de Azure Cosmos con hello API de documentos</span><span class="sxs-lookup"><span data-stu-id="4f196-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="4f196-104">[Base de datos de Microsoft Azure Cosmos](../cosmos-db/introduction.md) es un toohelp de servicio diseñado de base de datos distribuida, varios modelos global, obtendrá rendimiento rápido y predecible y escalabilidad sin problemas junto con la aplicación que se incremente.</span><span class="sxs-lookup"><span data-stu-id="4f196-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="4f196-105">Este artículo proporciona información general sobre cómo toowork con las particiones de base de datos de Cosmos contenedores con Hola API de documentos.</span><span class="sxs-lookup"><span data-stu-id="4f196-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4f196-106">Consulte [la creación de particiones y el escalado horizontal](../cosmos-db/partition-data.md) para obtener una información general de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f196-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="4f196-107">tooget a trabajar con código, descargue el proyecto Hola de [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4f196-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="4f196-108">Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="4f196-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="4f196-109">¿Cómo funcionan las particiones en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="4f196-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="4f196-110">¿Cómo se configuran las particiones en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="4f196-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="4f196-111">¿Cuáles son las claves de partición y cómo seleccionar clave de partición correcta de Hola para mi aplicación?</span><span class="sxs-lookup"><span data-stu-id="4f196-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="4f196-112">tooget a trabajar con código, descargue el proyecto Hola de [ejemplo de la controlador de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4f196-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="4f196-113">Claves de partición</span><span class="sxs-lookup"><span data-stu-id="4f196-113">Partition keys</span></span>

<span data-ttu-id="4f196-114">En hello API de documentos, puede especificar la definición de clave de partición de hello en forma de Hola de una ruta de acceso JSON.</span><span class="sxs-lookup"><span data-stu-id="4f196-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="4f196-115">Hello tabla siguiente muestran ejemplos de definiciones de clave de partición y valores de hello correspondientes tooeach.</span><span class="sxs-lookup"><span data-stu-id="4f196-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="4f196-116">clave de partición de Hola se especifica como una ruta de acceso, por ejemplo, `/department` representa Hola departamento de propiedad.</span><span class="sxs-lookup"><span data-stu-id="4f196-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f196-117"><strong>Clave de partición</strong></span><span class="sxs-lookup"><span data-stu-id="4f196-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f196-118"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="4f196-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f196-119">/department</span><span class="sxs-lookup"><span data-stu-id="4f196-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f196-120">Corresponde toohello valo doc.department donde doc es elemento Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f196-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="4f196-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f196-122">Corresponde toohello valo doc.properties.name donde doc es elemento hello (propiedad anidada).</span><span class="sxs-lookup"><span data-stu-id="4f196-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f196-123">/id</span><span class="sxs-lookup"><span data-stu-id="4f196-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f196-124">Corresponde toohello valo doc.id (clave de identificador y la partición se Hola misma propiedad).</span><span class="sxs-lookup"><span data-stu-id="4f196-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f196-125">/"nombre de departamento"</span><span class="sxs-lookup"><span data-stu-id="4f196-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f196-126">Corresponde toohello valo doc ["nombre de departamento"] donde doc es elemento Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="4f196-127">sintaxis de Hola de clave de partición es similar especificación de ruta de acceso de toohello para indizar rutas de acceso de directiva con la diferencia clave Hola que Hola ruta de acceso correspondiente propiedad toohello en lugar del valor de hello, es decir, no es ningún carácter comodín al final de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="4f196-128">¿Por ejemplo, especificaría /department/?</span><span class="sxs-lookup"><span data-stu-id="4f196-128">For example, you would specify /department/?</span></span> <span data-ttu-id="4f196-129">Hola tooindex valores en departamento, pero especifique /department como definición de clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="4f196-130">clave de partición de Hello está indexada de forma implícita y no se puede excluir de la indización mediante invalidaciones de directiva de indización.</span><span class="sxs-lookup"><span data-stu-id="4f196-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="4f196-131">Echemos un vistazo a la elección de Hola de clave de partición afecta al rendimiento de hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f196-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="4f196-132">Trabajar con hello Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="4f196-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="4f196-133">A partir de la [versión de la API de REST de 16-12-2015](/rest/api/documentdb/), Azure Cosmos DB admite la creación automática de particiones.</span><span class="sxs-lookup"><span data-stu-id="4f196-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="4f196-134">Admite más reciente en uno de Hola o en contenedores de orden toocreate particionado, debe descargar las versiones del SDK 1.6.0 plataformas SDK (. NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="4f196-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="4f196-135">Creación de contenedores</span><span class="sxs-lookup"><span data-stu-id="4f196-135">Creating containers</span></span>
<span data-ttu-id="4f196-136">Hello en el ejemplo siguiente se muestra un toocreate de fragmento de código de .NET un contenedor toostore dispositivo los datos de telemetría de 20.000 unidades de solicitud por segundo de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="4f196-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="4f196-137">Hola SDK establece el valor de OfferThroughput de hello (que a su vez establece hello `x-ms-offer-throughput` encabezado de solicitud de hello API de REST).</span><span class="sxs-lookup"><span data-stu-id="4f196-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="4f196-138">A continuación establecemos hello `/deviceId` como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="4f196-139">opción de Hola de clave de partición se guarda junto con el resto de Hola de hello metadatos del contenedor como nombre y la directiva de indexación.</span><span class="sxs-lookup"><span data-stu-id="4f196-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="4f196-140">Para este ejemplo, se seleccionarán `deviceId` puesto que sabemos que (a) puesto que hay un gran número de dispositivos, escrituras se pueden distribuir en particiones uniformemente y lo que nos tooscale Hola tooingest grandes volúmenes de datos de base de datos y (b) muchas de las solicitudes de hello como obtención de lectura más reciente de Hola para un dispositivo son tooa ámbito único deviceId y pueden obtenerse de una sola partición.</span><span class="sxs-lookup"><span data-stu-id="4f196-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

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

<span data-ttu-id="4f196-141">Este método realiza una API de REST llamada tooCosmos base de datos y servicio Hola proporcionará un número de particiones según rendimiento solicitado Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="4f196-142">Puede cambiar el rendimiento de un contenedor de hello según sus necesidades de rendimiento evolucionan.</span><span class="sxs-lookup"><span data-stu-id="4f196-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="4f196-143">Lectura y escritura de elementos</span><span class="sxs-lookup"><span data-stu-id="4f196-143">Reading and writing items</span></span>
<span data-ttu-id="4f196-144">Ahora, insertemos los datos en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f196-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="4f196-145">Esta es una clase de ejemplo que contiene una lectura de dispositivo y un tooinsert de tooCreateDocumentAsync de llamada a un nuevo dispositivo de lectura en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="4f196-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="4f196-146">Este es un ejemplo que aprovecha Hola API de documentos:</span><span class="sxs-lookup"><span data-stu-id="4f196-146">This is an example leveraging hello DocumentDB API:</span></span>

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

<span data-ttu-id="4f196-147">Vamos a leer el elemento Hola por su clave de partición y el Id., actualizar y como paso final, elimínela identificador y la clave de partición. Tenga en cuenta que las lecturas Hola incluyen un valor de PartitionKey (toohello correspondiente `x-ms-documentdb-partitionkey` encabezado de solicitud de hello API de REST).</span><span class="sxs-lookup"><span data-stu-id="4f196-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="4f196-148">Consulta de contenedores con particiones</span><span class="sxs-lookup"><span data-stu-id="4f196-148">Querying partitioned containers</span></span>
<span data-ttu-id="4f196-149">Al consultar los datos en contenedores con particiones, base de datos de Cosmos automáticamente las rutas Hola particiones toohello de consulta correspondiente a los valores de clave de partición de toohello especificados en el filtro de hello (si hay alguno).</span><span class="sxs-lookup"><span data-stu-id="4f196-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="4f196-150">Por ejemplo, esta consulta es la clave de partición Hola de contenedor de partición de hello del toojust enrutado "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="4f196-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="4f196-151">Hola siguiente consulta no tiene un filtro en la clave de partición de hello (DeviceId) y es en abanico particiones tooall donde se ejecuta en el índice de la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="4f196-152">Tenga en cuenta que tener hello toospecify EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` Hola API de REST) toohave Hola SDK tooexecute una consulta en particiones.</span><span class="sxs-lookup"><span data-stu-id="4f196-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="4f196-153">Cosmos DB admite las [funciones de agregado](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` y `AVG` en contenedores con particiones mediante SQL a partir del SDK 1.12.0, y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="4f196-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="4f196-154">Las consultas deben incluir un operador agregado único y deben incluir un valor único en la proyección de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f196-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="4f196-155">Ejecución de consultas en paralelo</span><span class="sxs-lookup"><span data-stu-id="4f196-155">Parallel query execution</span></span>
<span data-ttu-id="4f196-156">Hola Cosmos DB SDK 1.9.0 y versiones posteriores admite opciones de ejecución de consultas en paralelo, lo que permite una latencia baja tooperform consultas en colecciones con particiones, incluso cuando los necesitan tootouch un gran número de particiones.</span><span class="sxs-lookup"><span data-stu-id="4f196-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="4f196-157">Por ejemplo, hello después de consulta es toorun configurado en paralelo en particiones.</span><span class="sxs-lookup"><span data-stu-id="4f196-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="4f196-158">Puede administrar la ejecución de consultas en paralelo ajustando Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f196-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="4f196-159">Estableciendo `MaxDegreeOfParallelism`, puede controlar el grado de Hola de paralelismo, es decir, Hola número máximo de particiones del contenedor de las toohello de conexiones de red simultáneas.</span><span class="sxs-lookup"><span data-stu-id="4f196-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="4f196-160">Si se establece demasiado-1, se administra el grado de paralelismo Hola Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="4f196-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="4f196-161">Si hello `MaxDegreeOfParallelism` no se ha especificado o establecer too0, que es el valor predeterminado de hello, habrá particiones del contenedor toohello de conexión de red único.</span><span class="sxs-lookup"><span data-stu-id="4f196-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="4f196-162">Al establecer `MaxBufferedItemCount`, puede compensar el uso de memoria por parte del cliente y la latencia en las consultas.</span><span class="sxs-lookup"><span data-stu-id="4f196-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="4f196-163">Si omite este parámetro o se establece demasiado-1, número de Hola de elementos almacenados en búfer durante la ejecución de consultas en paralelo es administrado por hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4f196-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="4f196-164">Dados Hola mismo estado de recopilación de hello, una consulta en paralelo devolverá resultados Hola mismo pedido como en ejecución en serie.</span><span class="sxs-lookup"><span data-stu-id="4f196-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="4f196-165">Al realizar una consulta entre particiones que incluye la ordenación (ORDER BY o superior), problemas de SDK de base de datos de Azure Cosmos Hola Hola consulta en paralelo a través de las particiones y combinaciones resultados parcialmente ordenados en tooproduce de lado cliente hello resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="4f196-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="4f196-166">Ejecución de procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="4f196-166">Executing stored procedures</span></span>
<span data-ttu-id="4f196-167">También puede ejecutar transacciones atómicas con documentos con Hola mismo Id. de dispositivo, por ejemplo, si desea mantener agregados u Hola estado más reciente de un dispositivo en un único elemento.</span><span class="sxs-lookup"><span data-stu-id="4f196-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="4f196-168">En la siguiente sección hello, veremos cómo puede trasladar toopartitioned contenedores de contenedores de partición única.</span><span class="sxs-lookup"><span data-stu-id="4f196-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f196-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f196-169">Next steps</span></span>
<span data-ttu-id="4f196-170">En este artículo, se proporciona información general sobre cómo toowork con las particiones de base de datos de Azure Cosmos contenedores con Hola API de documentos.</span><span class="sxs-lookup"><span data-stu-id="4f196-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4f196-171">Consulte también [la creación de particiones y el escalado horizontal](../cosmos-db/partition-data.md) para obtener una información general de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f196-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="4f196-172">Realice pruebas de escala y de rendimiento con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f196-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="4f196-173">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md) para ver ejemplos.</span><span class="sxs-lookup"><span data-stu-id="4f196-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="4f196-174">Comenzar a codificar con hello [SDK](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="4f196-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="4f196-175">Información sobre el [procesamiento aprovisionado en Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="4f196-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

