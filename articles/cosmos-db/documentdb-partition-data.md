---
title: "Creación de particiones y escalado en Azure Cosmos DB | Microsoft Docs"
description: "Obtenga información sobre cómo funciona la creación de particiones en Azure Cosmos DB, cómo configurar la creación de particiones y las claves de partición y cómo seleccionar la clave de partición correcta para su aplicación."
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
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="ccd17-103">Creación de particiones en Azure Cosmos DB con la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ccd17-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="ccd17-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos distribuido de varios modelos global diseñado para ayudarle a lograr un rendimiento rápido y predecible. Además, permite escalar sin problemas a medida que la aplicación crece.</span><span class="sxs-lookup"><span data-stu-id="ccd17-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="ccd17-105">En este artículo se proporciona información general sobre cómo trabajar con las particiones de contenedores de Cosmos DB con la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ccd17-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="ccd17-106">Consulte [la creación de particiones y el escalado horizontal](../cosmos-db/partition-data.md) para obtener una información general de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccd17-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="ccd17-107">Para empezar a trabajar con código, descargue el proyecto de [GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="ccd17-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="ccd17-108">Después de leer este artículo, podrá responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="ccd17-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="ccd17-109">¿Cómo funcionan las particiones en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="ccd17-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="ccd17-110">¿Cómo se configuran las particiones en Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="ccd17-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="ccd17-111">¿Qué son las claves de partición y cómo se elige la clave de partición correcta para una aplicación?</span><span class="sxs-lookup"><span data-stu-id="ccd17-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="ccd17-112">Para empezar a trabajar con código, descargue el proyecto del [ejemplo de versión de prueba de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="ccd17-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="ccd17-113">Claves de partición</span><span class="sxs-lookup"><span data-stu-id="ccd17-113">Partition keys</span></span>

<span data-ttu-id="ccd17-114">En la API de DocumentDB, especifique la definición de la clave de partición en el formulario de una ruta de acceso JSON.</span><span class="sxs-lookup"><span data-stu-id="ccd17-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="ccd17-115">En la tabla siguiente se muestran ejemplos de definiciones de clave de partición y los valores correspondientes a cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="ccd17-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="ccd17-116">La clave de partición se especifica como una ruta de acceso; por ejemplo, `/department` representa el departamento de propiedad.</span><span class="sxs-lookup"><span data-stu-id="ccd17-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="ccd17-117"><strong>Clave de partición</strong></span><span class="sxs-lookup"><span data-stu-id="ccd17-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ccd17-118"><strong>Descripción</strong></span><span class="sxs-lookup"><span data-stu-id="ccd17-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ccd17-119">/department</span><span class="sxs-lookup"><span data-stu-id="ccd17-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ccd17-120">Corresponde al valor de doc.department, donde doc es el elemento.</span><span class="sxs-lookup"><span data-stu-id="ccd17-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ccd17-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="ccd17-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ccd17-122">Corresponde al valor de doc.properties.name, donde doc es el elemento (propiedad anidada).</span><span class="sxs-lookup"><span data-stu-id="ccd17-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ccd17-123">/id</span><span class="sxs-lookup"><span data-stu-id="ccd17-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ccd17-124">Corresponde al valor de doc.id (el identificador y la clave de partición son la misma propiedad).</span><span class="sxs-lookup"><span data-stu-id="ccd17-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ccd17-125">/"nombre de departamento"</span><span class="sxs-lookup"><span data-stu-id="ccd17-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ccd17-126">Corresponde al valor de doc["nombre de departamento"], donde doc es el elemento.</span><span class="sxs-lookup"><span data-stu-id="ccd17-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="ccd17-127">La sintaxis de la clave de partición es similar a la especificación de rutas de acceso para la indexación de rutas de acceso de directivas con la importante diferencia de que la ruta de acceso corresponde a la propiedad en lugar de al valor, es decir, no hay ningún carácter comodín al final.</span><span class="sxs-lookup"><span data-stu-id="ccd17-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="ccd17-128">¿Por ejemplo, especificaría /department/?</span><span class="sxs-lookup"><span data-stu-id="ccd17-128">For example, you would specify /department/?</span></span> <span data-ttu-id="ccd17-129">para indexar los valores bajo departament, pero especificaría /department como la definición de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="ccd17-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="ccd17-130">La clave de partición está indexada de forma implícita y no se puede excluir de la indexación mediante invalidaciones de directiva de indexación.</span><span class="sxs-lookup"><span data-stu-id="ccd17-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="ccd17-131">Examinemos cómo afecta la elección de la clave de partición al rendimiento de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccd17-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="ccd17-132">Uso de los SDK de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ccd17-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="ccd17-133">A partir de la [versión de la API de REST de 16-12-2015](/rest/api/documentdb/), Azure Cosmos DB admite la creación automática de particiones.</span><span class="sxs-lookup"><span data-stu-id="ccd17-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="ccd17-134">Para poder crear contenedores con particiones, es necesario descargar la versión del SDK 1.6.0 (o posteriores) en una de las plataformas admitidas del SDK (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="ccd17-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="ccd17-135">Creación de contenedores</span><span class="sxs-lookup"><span data-stu-id="ccd17-135">Creating containers</span></span>
<span data-ttu-id="ccd17-136">En el ejemplo siguiente se muestra un fragmento de código .NET mediante el que se crea un contenedor que almacena los datos de telemetría de dispositivos con un procesamiento de 20 000 unidades de solicitud por segundo.</span><span class="sxs-lookup"><span data-stu-id="ccd17-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="ccd17-137">El SDK establece el valor OfferThroughput (que a su vez establece el encabezado de solicitud `x-ms-offer-throughput` en la API de REST).</span><span class="sxs-lookup"><span data-stu-id="ccd17-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="ccd17-138">En este caso, la clave de partición es `/deviceId` .</span><span class="sxs-lookup"><span data-stu-id="ccd17-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="ccd17-139">La elección de la clave de partición se guarda junto con el resto de los metadatos del contenedor, como nombre y la directiva de indexación.</span><span class="sxs-lookup"><span data-stu-id="ccd17-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="ccd17-140">Para este ejemplo, elegimos `deviceId` por dos motivos: en primer lugar, sabemos que al haber un gran número de dispositivos, las escrituras pueden distribuirse entre las particiones de manera uniforme, lo que nos permite escalar la base de datos para introducir grandes volúmenes de datos; en segundo lugar, muchas de las solicitudes, como la obtención de la última lectura correspondiente a un dispositivo, se limitan a un único deviceId y se pueden recuperar desde una única partición.</span><span class="sxs-lookup"><span data-stu-id="ccd17-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

<span data-ttu-id="ccd17-141">Este método realiza una llamada API de REST a Cosmos DB, tras lo cual el servicio proporciona un número de particiones que está determinado en función del procesamiento que se solicite.</span><span class="sxs-lookup"><span data-stu-id="ccd17-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="ccd17-142">Puede cambiar el procesamiento de un contenedor a medida que evolucionen sus necesidades de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ccd17-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="ccd17-143">Lectura y escritura de elementos</span><span class="sxs-lookup"><span data-stu-id="ccd17-143">Reading and writing items</span></span>
<span data-ttu-id="ccd17-144">Ahora, insertemos los datos en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccd17-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="ccd17-145">La clase de ejemplo siguiente contiene una lectura de dispositivo y una llamada a CreateDocumentAsync para insertar una nueva lectura de dispositivo en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="ccd17-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="ccd17-146">Este es un ejemplo que aprovecha la API de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="ccd17-146">This is an example leveraging the DocumentDB API:</span></span>

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

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
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

<span data-ttu-id="ccd17-147">A continuación leeremos el elemento por su clave de partición e identificador, lo actualizaremos y, como paso final, lo eliminaremos por la clave de partición e identificador. Tenga en cuenta que las lecturas incluyen un valor PartitionKey (correspondiente al encabezado de solicitud `x-ms-documentdb-partitionkey` de la API de REST).</span><span class="sxs-lookup"><span data-stu-id="ccd17-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="ccd17-148">Consulta de contenedores con particiones</span><span class="sxs-lookup"><span data-stu-id="ccd17-148">Querying partitioned containers</span></span>
<span data-ttu-id="ccd17-149">Al consultar datos en los contenedores con particiones, Azure Cosmos DB enruta automáticamente la consulta a las particiones correspondientes a los valores de clave de partición especificados en el filtro (en caso de que los haya).</span><span class="sxs-lookup"><span data-stu-id="ccd17-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="ccd17-150">Por ejemplo, esta consulta se enruta únicamente a la partición cuya clave es "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="ccd17-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="ccd17-151">La consulta siguiente no tiene filtro en la clave de partición (DeviceId) y por ello se despliega por todas las particiones, en las que se ejecuta según el índice de la partición.</span><span class="sxs-lookup"><span data-stu-id="ccd17-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="ccd17-152">Tenga en cuenta que debe especificar EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` en la API de REST) para que el SDK ejecute una consulta en todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="ccd17-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="ccd17-153">Cosmos DB admite las [funciones de agregado](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` y `AVG` en contenedores con particiones mediante SQL a partir del SDK 1.12.0, y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="ccd17-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="ccd17-154">Las consultas deben incluir un único operador de agregado y deben incluir un valor individual en la proyección.</span><span class="sxs-lookup"><span data-stu-id="ccd17-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="ccd17-155">Ejecución de consultas en paralelo</span><span class="sxs-lookup"><span data-stu-id="ccd17-155">Parallel query execution</span></span>
<span data-ttu-id="ccd17-156">Los SDK de Cosmos DB de la versión 1.9.0 y posterior admiten opciones de ejecución de consultas en paralelo, que permiten realizar consultas de baja latencia en colecciones con particiones, incluso cuando tienen que acceder a un gran número de particiones.</span><span class="sxs-lookup"><span data-stu-id="ccd17-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="ccd17-157">Por ejemplo, la siguiente consulta está configurada para ejecutarse en paralelo en particiones.</span><span class="sxs-lookup"><span data-stu-id="ccd17-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="ccd17-158">Puede administrar la ejecución de consultas en paralelo ajustando los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="ccd17-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="ccd17-159">Al establecer `MaxDegreeOfParallelism`, puede controlar el grado de paralelismo; es decir, el número máximo de conexiones de red simultáneas en las particiones del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ccd17-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="ccd17-160">Si lo establece en -1, el grado de paralelismo lo administra el SDK.</span><span class="sxs-lookup"><span data-stu-id="ccd17-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="ccd17-161">Si el parámetro `MaxDegreeOfParallelism` no se especifica o está establecido en 0, que es el valor predeterminado, habrá una única conexión de red a las particiones del contenedor.</span><span class="sxs-lookup"><span data-stu-id="ccd17-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="ccd17-162">Al establecer `MaxBufferedItemCount`, puede compensar el uso de memoria por parte del cliente y la latencia en las consultas.</span><span class="sxs-lookup"><span data-stu-id="ccd17-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="ccd17-163">Si se omite este parámetro o lo establece en -1, el número de elementos almacenados en búfer durante la ejecución de consultas en paralelo lo administrará el SDK.</span><span class="sxs-lookup"><span data-stu-id="ccd17-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="ccd17-164">Como se trata del mismo estado de la colección, una consulta en paralelo devolverá resultados en el mismo orden que la ejecución en serie.</span><span class="sxs-lookup"><span data-stu-id="ccd17-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="ccd17-165">Al realizar una consulta entre particiones que incluye la ordenación (ORDER BY o TOP), el SDK de Azure Cosmos DB emite la consulta en paralelo entre las particiones y combina los resultados ordenados parcialmente en el lado del cliente para generar resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="ccd17-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="ccd17-166">Ejecución de procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="ccd17-166">Executing stored procedures</span></span>
<span data-ttu-id="ccd17-167">También puede ejecutar transacciones atómicas en relación con documentos con el mismo identificador de dispositivo, por ejemplo, si desea mantener los agregados o el estado más reciente de un dispositivo en un único elemento.</span><span class="sxs-lookup"><span data-stu-id="ccd17-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="ccd17-168">En la siguiente sección, veremos cómo puede moverse a contenedores con particiones desde contenedores de partición única.</span><span class="sxs-lookup"><span data-stu-id="ccd17-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd17-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccd17-169">Next steps</span></span>
<span data-ttu-id="ccd17-170">En este artículo se proporciona información general sobre cómo trabajar con las particiones de contenedores de Azure Cosmos DB con la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ccd17-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="ccd17-171">Consulte también [la creación de particiones y el escalado horizontal](../cosmos-db/partition-data.md) para obtener una información general de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccd17-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="ccd17-172">Realice pruebas de escala y de rendimiento con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccd17-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="ccd17-173">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md) para ver ejemplos.</span><span class="sxs-lookup"><span data-stu-id="ccd17-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="ccd17-174">Introducción a la codificación con [SDK](documentdb-sdk-dotnet.md) o la [API de REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="ccd17-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="ccd17-175">Información sobre el [procesamiento aprovisionado en Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="ccd17-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

