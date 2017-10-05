---
title: Compatibilidad con la fuente de cambios en Azure Cosmos DB | Microsoft Docs
description: "Use la compatibilidad con la fuente de cambios de Azure Cosmos DB para controlar los cambios en documentos y realizar el procesamiento basado en eventos tales como desencadenadores y mantener actualizados las cachés y los sistemas de análisis."
keywords: fuente de cambios
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="80f09-104">Compatibilidad con la fuente de cambios en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80f09-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="80f09-105">[Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos rápido y flexible, replicado globalmente, que se usa para almacenar elevados volúmenes de datos de transacciones y operaciones con una latencia predecible inferior a 10 milisegundos en lecturas y escrituras.</span><span class="sxs-lookup"><span data-stu-id="80f09-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="80f09-106">Esto hace que sea adecuado para IoT, juegos y aplicaciones de registro de operaciones.</span><span class="sxs-lookup"><span data-stu-id="80f09-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="80f09-107">Un patrón de diseño habitual en estas aplicaciones es controlar los cambios realizados en datos de Azure Cosmos DB y actualizar las vistas materializadas, realizar análisis en tiempo real, archivar los datos en almacenamiento en frío y desencadenar notificaciones ante determinados eventos en función de estos cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="80f09-108">La **compatibilidad con la fuente de cambios** en Azure Cosmos DB le permite crear soluciones eficientes y escalables para cada uno de estos patrones.</span><span class="sxs-lookup"><span data-stu-id="80f09-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="80f09-109">Gracias a la compatibilidad con la fuente de cambios, Azure Cosmos DB proporciona una lista ordenada de documentos de una colección de Azure Cosmos DB en el orden en que se modificaron.</span><span class="sxs-lookup"><span data-stu-id="80f09-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="80f09-110">Esta fuente se puede usar para estar al tanto de las modificaciones en los datos dentro de la colección y realizar acciones tales como:</span><span class="sxs-lookup"><span data-stu-id="80f09-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="80f09-111">Desencadenar una llamada a una API cuando se inserta o modifica un documento</span><span class="sxs-lookup"><span data-stu-id="80f09-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="80f09-112">Realizar el procesamiento en tiempo real (secuencia) sobre las actualizaciones</span><span class="sxs-lookup"><span data-stu-id="80f09-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="80f09-113">Sincronizar datos con una caché, un motor de búsqueda o un almacén de datos</span><span class="sxs-lookup"><span data-stu-id="80f09-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="80f09-114">Los cambios en Azure Cosmos DB se conservan y se pueden procesar de manera asincrónica y distribuirse entre uno o varios clientes para un procesamiento en paralelo.</span><span class="sxs-lookup"><span data-stu-id="80f09-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="80f09-115">Echemos un vistazo a las API de fuente de cambios y cómo se pueden usar para crear soluciones en tiempo real escalables.</span><span class="sxs-lookup"><span data-stu-id="80f09-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="80f09-116">En este artículo se muestra cómo trabajar con la fuente de cambios de Azure Cosmos DB y la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="80f09-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Uso de la fuente de cambios de Azure Cosmos DB para aumentar la eficacia de los escenarios de informática orientada a eventos y análisis en tiempo real](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="80f09-118">En este momento, solo se ofrece compatibilidad con la fuente de cambios para la API de DocumentDB; la API Graph y Table API no se admiten actualmente.</span><span class="sxs-lookup"><span data-stu-id="80f09-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="80f09-119">Casos de uso y escenarios</span><span class="sxs-lookup"><span data-stu-id="80f09-119">Use cases and scenarios</span></span>
<span data-ttu-id="80f09-120">La fuente de cambios permite procesar con eficacia grandes conjuntos de datos con un elevado volumen de escrituras, y ofrece una alternativa a la consulta de conjuntos de datos enteros para identificar lo que ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="80f09-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="80f09-121">Por ejemplo, puede realizar las siguientes tareas de manera eficaz:</span><span class="sxs-lookup"><span data-stu-id="80f09-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="80f09-122">Actualizar una caché, un índice de búsqueda o un almacenamiento de datos con los datos almacenados en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="80f09-123">Implementar archivado y niveles de datos de aplicación, es decir, almacenar "datos activos" en Azure Cosmos DB y "jubilar datos inactivos" en [Azure Blob Storage](../storage/common/storage-introduction.md) o [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80f09-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="80f09-124">Implementar análisis por lotes sobre los datos mediante [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="80f09-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="80f09-125">Implementar [canalizaciones Lambda en Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="80f09-126">Azure Cosmos DB proporciona una solución de base de datos escalable que puede hacer frente tanto a la ingesta como a la consulta, e implementar arquitecturas Lambda con un bajo TCO.</span><span class="sxs-lookup"><span data-stu-id="80f09-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="80f09-127">Realizar migraciones con cero tiempo de inactividad a otra cuenta de Azure Cosmos DB con otro esquema de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="80f09-128">**Canalizaciones Lambda con Azure Cosmos DB para ingesta y consulta:**</span><span class="sxs-lookup"><span data-stu-id="80f09-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Canalización Lambda basada en Azure Cosmos DB para ingesta y consulta](./media/change-feed/lambda.png)

<span data-ttu-id="80f09-130">Puede usar Azure Cosmos DB para recibir y almacenar datos de eventos de dispositivos, sensores, infraestructuras y aplicaciones y luego procesarlos en tiempo real con [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md) o [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80f09-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="80f09-131">En las aplicaciones web y móviles [sin servidor](http://azure.com/serverless), puede realizar el seguimiento de eventos, como cambios en el perfil del cliente, preferencias o ubicación para desencadenar determinadas acciones como enviar notificaciones push a sus dispositivos mediante [Azure Functions](../azure-functions/functions-bindings-documentdb.md) o [App Services](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="80f09-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="80f09-132">Si usa Azure Cosmos DB para compilar un juego, puede usar la fuente de cambios para, por ejemplo, implementar marcadores en tiempo real basados en las puntuaciones de los juegos completados.</span><span class="sxs-lookup"><span data-stu-id="80f09-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="80f09-133">Funcionamiento de la fuente de cambios en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80f09-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="80f09-134">Azure Cosmos DB ofrece la posibilidad de leer las actualizaciones realizadas de manera incremental en una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="80f09-135">Esta fuente de cambios tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="80f09-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="80f09-136">Los cambios son persistentes en Azure Cosmos DB y pueden procesarse de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="80f09-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="80f09-137">Los cambios en los documentos dentro de una colección están disponibles inmediatamente en la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="80f09-138">Cada cambio realizado en un documento aparece exactamente una vez en la fuente de cambios y los clientes administran su lógica de puntos de comprobación.</span><span class="sxs-lookup"><span data-stu-id="80f09-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="80f09-139">La biblioteca de procesadores de fuentes de cambio proporciona semántica de puntos de comprobación automáticos y "al menos una vez".</span><span class="sxs-lookup"><span data-stu-id="80f09-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="80f09-140">Solo el cambio más reciente en un documento determinado se incluye en el registro de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="80f09-141">Puede que los cambios intermedios no estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="80f09-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="80f09-142">La fuente de cambios está clasificada por orden de modificación dentro de cada valor de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="80f09-143">No hay ningún orden garantizado entre valores de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="80f09-144">Los cambios se pueden sincronizar desde cualquier punto en el tiempo, es decir, no hay ningún período fijo de retención de datos en el que los cambios estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="80f09-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="80f09-145">Los cambios están disponibles en fragmentos de intervalos de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="80f09-146">Esta funcionalidad permite que los cambios de colecciones grandes se procesen en paralelo por medio de varios consumidores/servidores.</span><span class="sxs-lookup"><span data-stu-id="80f09-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="80f09-147">Las aplicaciones pueden solicitar varias fuentes de cambios a la vez en la misma colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="80f09-148">La fuente de cambios de Azure DB Cosmos está habilitada de forma predeterminada para todas las cuentas.</span><span class="sxs-lookup"><span data-stu-id="80f09-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="80f09-149">Puede usar el [procesamiento aprovisionado](request-units.md) en su región de escritura o en cualquier [región de lectura](distribute-data-globally.md) para leer la fuente de cambios, igual que con cualquier otra operación de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="80f09-150">La fuente de cambios incluye inserciones y operaciones de actualización realizadas en los documentos dentro de la colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="80f09-151">Puede capturar eliminaciones estableciendo un indicador "eliminación temporal" dentro de los documentos en lugar de eliminaciones.</span><span class="sxs-lookup"><span data-stu-id="80f09-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="80f09-152">Como alternativa, puede establecer un período finito de caducidad para los documentos mediante la [funcionalidad TTL](time-to-live.md), por ejemplo, 24 horas, y usar el valor de esa propiedad para capturar las eliminaciones.</span><span class="sxs-lookup"><span data-stu-id="80f09-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="80f09-153">Con esta solución, tiene que procesar los cambios dentro de un intervalo de tiempo más corto que el período de expiración de TTL.</span><span class="sxs-lookup"><span data-stu-id="80f09-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="80f09-154">La fuente de cambios está disponible para cada intervalo de claves de partición dentro de la colección de documentos y, por tanto, se puede distribuir entre uno o varios consumidores para el procesamiento en paralelo.</span><span class="sxs-lookup"><span data-stu-id="80f09-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Procesamiento distribuido de la fuente de cambios de Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="80f09-156">Tiene algunas opciones para implementar una fuente de cambios en el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="80f09-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="80f09-157">En las secciones siguientes se describe cómo implementar la fuente de cambios mediante la API de REST de Azure Cosmos DB y los SDK de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="80f09-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="80f09-158">Sin embargo, para las aplicaciones. NET, se recomienda usar la nueva [biblioteca de procesadores de fuentes de cambio](#change-feed-processor) para procesar los eventos de la fuente de cambios, ya que simplifica la lectura de los cambios en las distintas particiones y permite varios subprocesos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="80f09-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="80f09-159"><a id="rest-apis"></a>Trabajo con la API de REST y los SDK de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="80f09-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="80f09-160">Azure Cosmos DB proporciona contenedores elásticos de almacenamiento y rendimiento denominados **colecciones**.</span><span class="sxs-lookup"><span data-stu-id="80f09-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="80f09-161">Los datos dentro de las colecciones están agrupados de manera lógica mediante [claves de partición](partition-data.md) para mejorar la escalabilidad y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="80f09-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="80f09-162">Azure Cosmos DB proporciona varias API para acceder a estos datos, entre las que se incluyen búsqueda por identificador (leer/obtener), consulta y fuentes de lectura (exámenes).</span><span class="sxs-lookup"><span data-stu-id="80f09-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="80f09-163">La fuente de cambios se puede obtener rellenando dos nuevos encabezados de solicitud para la API `ReadDocumentFeed` de DocumentDB; luego se puede procesar en paralelo entre intervalos de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="80f09-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="80f09-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="80f09-165">Examinemos brevemente cómo funciona ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="80f09-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="80f09-166">Azure Cosmos DB admite la lectura de una fuente de documentos dentro de una colección mediante la API `ReadDocumentFeed`.</span><span class="sxs-lookup"><span data-stu-id="80f09-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="80f09-167">Por ejemplo, la siguiente solicitud devuelve una página de documentos dentro de la colección `serverlogs`.</span><span class="sxs-lookup"><span data-stu-id="80f09-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="80f09-168">Se pueden limitar los resultados mediante el encabezado `x-ms-max-item-count`, y se pueden resumir las lecturas reenviando la solicitud con un encabezado `x-ms-continuation` devuelto en la respuesta anterior.</span><span class="sxs-lookup"><span data-stu-id="80f09-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="80f09-169">Cuando se realiza desde un único cliente, `ReadDocumentFeed` realiza la iteración de los resultados entre particiones en serie.</span><span class="sxs-lookup"><span data-stu-id="80f09-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="80f09-170">**Fuente de documento de lectura en serie**</span><span class="sxs-lookup"><span data-stu-id="80f09-170">**Serial read document feed**</span></span>

<span data-ttu-id="80f09-171">También puede recuperar la fuente de documentos mediante uno de los [SDK de Azure Cosmos DB](documentdb-sdk-dotnet.md) admitidos.</span><span class="sxs-lookup"><span data-stu-id="80f09-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="80f09-172">Por ejemplo, el fragmento de código siguiente muestra cómo usar el [método ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) en. NET.</span><span class="sxs-lookup"><span data-stu-id="80f09-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="80f09-173">Ejecución distribuida del ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="80f09-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="80f09-174">En el caso de colecciones que contienen terabytes de datos o mayores, o que realizan la ingesta de grandes volúmenes de actualizaciones, la ejecución en serie de la fuente de lectura desde una única máquina cliente puede que no sea una solución práctica.</span><span class="sxs-lookup"><span data-stu-id="80f09-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="80f09-175">Para estos escenarios de macrodatos, Azure Cosmos DB proporciona varias API que distribuyen las llamadas a `ReadDocumentFeed` de manera transparente entre varios lectores/consumidores cliente.</span><span class="sxs-lookup"><span data-stu-id="80f09-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="80f09-176">**Fuente de documentos de lectura distribuida**</span><span class="sxs-lookup"><span data-stu-id="80f09-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="80f09-177">Para proporcionar procesamiento escalable de cambios incrementales, Azure Cosmos DB admite un modelo de escalado horizontal para la API de fuente de cambios que se basa en intervalos de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="80f09-178">Puede obtener una lista de intervalos de claves de partición para una colección mediante la ejecución de una llamada a `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="80f09-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="80f09-179">Para cada intervalo de claves de partición, puede ejecutar una API `ReadDocumentFeed` para leer los documentos con las claves de partición incluidas dentro de ese intervalo.</span><span class="sxs-lookup"><span data-stu-id="80f09-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="80f09-180">Recuperación de los intervalos de claves de partición para una colección</span><span class="sxs-lookup"><span data-stu-id="80f09-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="80f09-181">Puede recuperar los intervalos de claves de partición solicitando el recurso `pkranges` dentro de una colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="80f09-182">Por ejemplo, la siguiente solicitud recupera la lista de intervalos de claves de partición para la colección `serverlogs`:</span><span class="sxs-lookup"><span data-stu-id="80f09-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="80f09-183">Esta solicitud devuelve la siguiente respuesta que contiene metadatos sobre los intervalos de claves de partición:</span><span class="sxs-lookup"><span data-stu-id="80f09-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="80f09-184">**Propiedades del intervalo de claves de partición**: cada intervalo de claves de partición incluye las propiedades de metadatos en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="80f09-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="80f09-185">Nombre de encabezado</span><span class="sxs-lookup"><span data-stu-id="80f09-185">Header name</span></span></th>
        <th><span data-ttu-id="80f09-186">Descripción</span><span class="sxs-lookup"><span data-stu-id="80f09-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-187">id</span><span class="sxs-lookup"><span data-stu-id="80f09-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="80f09-188">El identificador del intervalo de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-188">The ID for the partition key range.</span></span> <span data-ttu-id="80f09-189">Se trata de un identificador estable y único dentro de cada colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="80f09-190">Debe usarse en la llamada siguiente para leer los cambios por intervalo de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="80f09-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="80f09-192">El valor de hash de la clave de partición máxima para el intervalo de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="80f09-193">Solo para uso interno.</span><span class="sxs-lookup"><span data-stu-id="80f09-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="80f09-194">minInclusive</span></span></td>
        <td><span data-ttu-id="80f09-195">El valor de hash de clave de partición mínimo para el intervalo de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="80f09-196">Solo para uso interno.</span><span class="sxs-lookup"><span data-stu-id="80f09-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="80f09-197">Puede realizar esta tarea mediante uno de los [SDK de Azure Cosmos DB](documentdb-sdk-dotnet.md) admitidos.</span><span class="sxs-lookup"><span data-stu-id="80f09-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="80f09-198">Por ejemplo, el fragmento de código siguiente muestra cómo recuperar intervalos de claves de partición en. NET mediante el método [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="80f09-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="80f09-199">Azure Cosmos DB admite la recuperación de documentos por intervalo de claves de partición mediante el establecimiento del encabezado `x-ms-documentdb-partitionkeyrangeid` opcional.</span><span class="sxs-lookup"><span data-stu-id="80f09-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="80f09-200">Realización de una operación ReadDocumentFeed incremental</span><span class="sxs-lookup"><span data-stu-id="80f09-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="80f09-201">ReadDocumentFeed admite los siguientes escenarios o tareas para el procesamiento incremental de los cambios en las colecciones de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="80f09-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="80f09-202">Leer todos los cambios en los documentos desde el principio, es decir, desde la creación de la colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="80f09-203">Leer todos los cambios en las futuras actualizaciones de documentos desde el momento actual o los cambios desde un momento especificado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="80f09-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="80f09-204">Leer todos los cambios en los documentos desde una versión lógica de la colección (ETag).</span><span class="sxs-lookup"><span data-stu-id="80f09-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="80f09-205">Puede controlar a sus clientes según las etiquetas ETag devueltas por las solicitudes de fuente de lectura incremental.</span><span class="sxs-lookup"><span data-stu-id="80f09-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="80f09-206">Los cambios incluyen inserciones y actualizaciones de documentos.</span><span class="sxs-lookup"><span data-stu-id="80f09-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="80f09-207">Para capturar las eliminaciones, debe usar una propiedad de "eliminación temporal" dentro de los documentos, o bien la [propiedad TTL integrada](time-to-live.md) para señalar una eliminación pendiente en la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="80f09-208">En la tabla siguiente se muestran los [encabezados de solicitud](/rest/api/documentdb/common-documentdb-rest-request-headers.md) y [respuesta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para las operaciones ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="80f09-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="80f09-209">**Encabezados de solicitud para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="80f09-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="80f09-210">Nombre de encabezado</span><span class="sxs-lookup"><span data-stu-id="80f09-210">Header name</span></span></th>
        <th><span data-ttu-id="80f09-211">Descripción</span><span class="sxs-lookup"><span data-stu-id="80f09-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="80f09-212">A-IM</span></span></td>
        <td><span data-ttu-id="80f09-213">Debe establecerse en "fuente incremental" u omitirse.</span><span class="sxs-lookup"><span data-stu-id="80f09-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="80f09-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="80f09-215">Ningún encabezado: devuelve todos los cambios desde el principio (creación de la colección).</span><span class="sxs-lookup"><span data-stu-id="80f09-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="80f09-216">"*": devuelve todos los cambios nuevos en los datos dentro de la colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="80f09-217">&lt;etag&gt;: si está establecido en una ETag de colección, devuelve todos los cambios realizados desde esa marca de tiempo lógica.</span><span class="sxs-lookup"><span data-stu-id="80f09-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="80f09-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="80f09-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="80f09-219">Formato de hora RFC 1123; se omite si se especifica If-None-Match</span><span class="sxs-lookup"><span data-stu-id="80f09-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="80f09-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="80f09-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="80f09-221">Id. de intervalo de claves de partición para la lectura de datos.</span><span class="sxs-lookup"><span data-stu-id="80f09-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="80f09-222">**Encabezados de respuesta para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="80f09-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="80f09-223">Nombre de encabezado</span><span class="sxs-lookup"><span data-stu-id="80f09-223">Header name</span></span></th>
        <th><span data-ttu-id="80f09-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="80f09-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-225">ETag</span><span class="sxs-lookup"><span data-stu-id="80f09-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="80f09-226">El número de secuencia lógica (LSN) del último documento devuelto en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="80f09-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="80f09-227">La operación ReadDocumentFeed incremental se puede reanudar reenviando este valor en If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="80f09-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="80f09-228">Este es un ejemplo de solicitud para devolver todos los cambios incrementales realizados en la colección desde la versión lógica/ETag `28535` y el intervalo de claves de partición = `16`:</span><span class="sxs-lookup"><span data-stu-id="80f09-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="80f09-229">Los cambios están ordenados por tiempo dentro de cada valor de clave de partición del intervalo de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="80f09-230">No hay ningún orden garantizado entre valores de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="80f09-231">Si hay más resultados que pueden caber en una sola página, puede leer la página siguiente de resultados reenviando la solicitud con el encabezado `If-None-Match` con un valor igual a la etiqueta `etag` de la respuesta anterior.</span><span class="sxs-lookup"><span data-stu-id="80f09-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="80f09-232">Si varios documentos se han insertado o actualizado de manera transaccional dentro de un procedimiento almacenado o un desencadenador, todos se devolverán dentro de la misma página de respuesta.</span><span class="sxs-lookup"><span data-stu-id="80f09-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="80f09-233">Con la fuente de cambios, se pueden devolver más elementos en una página que los especificados en `x-ms-max-item-count` en el caso de que varios documentos se inserten o actualicen en los procedimientos almacenados o desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="80f09-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="80f09-234">Cuando use el SDK de .NET (1.17.0), establezca el campo `StartTime` en `ChangeFeedOptions` para devolver directamente los documentos cambiados desde `StartTime` al llamar a `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="80f09-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="80f09-235">Si especifica que `If-Modified-Since` use la API de REST, la solicitud devolverá no los propios documentos, sino más bien el token de continuación o `etag` en el encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="80f09-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="80f09-236">Para devolver los documentos modificados a la hora especificada, debe usarse el token de continuación `etag` en la siguiente solicitud con `If-None-Match` para devolver los documentos reales.</span><span class="sxs-lookup"><span data-stu-id="80f09-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="80f09-237">El SDK de .NET proporciona las clases auxiliares [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) y [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) para acceder a los cambios realizados en una colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="80f09-238">El fragmento de código siguiente muestra cómo recuperar todos los cambios desde el principio con el SDK de .NET desde un solo cliente.</span><span class="sxs-lookup"><span data-stu-id="80f09-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="80f09-239">Además, el fragmento de código siguiente muestra cómo procesar los cambios en tiempo real con Azure Cosmos DB mediante la compatibilidad con la fuente de cambios y la función anterior.</span><span class="sxs-lookup"><span data-stu-id="80f09-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="80f09-240">La primera llamada devuelve todos los documentos de la colección, y el segundo devuelve solo los dos documentos que se crearon desde el último punto de comprobación.</span><span class="sxs-lookup"><span data-stu-id="80f09-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="80f09-241">También puede filtrar la fuente de cambios usando la lógica del lado cliente para procesar los eventos de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="80f09-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="80f09-242">Por ejemplo, este es un fragmento de código LINQ del lado cliente para procesar solo los eventos de cambio de temperatura de los sensores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80f09-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="80f09-243"><a id="change-feed-processor"></a>Biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="80f09-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="80f09-244">Otra opción es usar la [biblioteca de procesadores de fuente de cambios de Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que puede ayudarle a distribuir el procesamiento de eventos fácilmente desde una fuente de cambios entre muchos consumidores.</span><span class="sxs-lookup"><span data-stu-id="80f09-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="80f09-245">La biblioteca es excelente para crear lectores de fuentes de cambios en la plataforma .NET.</span><span class="sxs-lookup"><span data-stu-id="80f09-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="80f09-246">Algunos flujos de trabajo que se simplificarían mediante la biblioteca de procesadores de fuente de cambios a través de los métodos incluidos en los otros SDK de Cosmos DB incluyen:</span><span class="sxs-lookup"><span data-stu-id="80f09-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="80f09-247">Extracción de actualizaciones de fuente de cambios cuando los datos se almacenan en varias particiones</span><span class="sxs-lookup"><span data-stu-id="80f09-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="80f09-248">Movimiento o replicación de datos de una colección a otra</span><span class="sxs-lookup"><span data-stu-id="80f09-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="80f09-249">Ejecución en paralelo de acciones desencadenadas por actualizaciones en datos y la fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="80f09-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="80f09-250">Mientras que el uso de las API en los SDK de Cosmos proporciona acceso a las actualizaciones de la fuente de cambios en cada partición, el uso de la biblioteca de procesadores de fuente de cambios simplifica la lectura de cambios en las particiones y en varios subprocesos que trabajen en paralelo.</span><span class="sxs-lookup"><span data-stu-id="80f09-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="80f09-251">En lugar de leer manualmente los cambios de cada contenedor y guardar un token de continuación para cada partición, el procesador de fuente de cambios administra automáticamente la lectura de los cambios en las particiones que usan un mecanismo de concesión.</span><span class="sxs-lookup"><span data-stu-id="80f09-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="80f09-252">La biblioteca está disponible como un paquete NuGet [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) y desde el código fuente como un [ejemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor) de Github.</span><span class="sxs-lookup"><span data-stu-id="80f09-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="80f09-253">Descripción de la biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="80f09-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="80f09-254">Hay cuatro componentes principales en la implementación del procesador de fuente de cambios: la colección supervisada, la colección de concesión, el host de procesador y los consumidores.</span><span class="sxs-lookup"><span data-stu-id="80f09-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="80f09-255">**Colección supervisada:** La colección supervisada consiste en los datos desde los que se genera la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="80f09-256">Todas las inserciones y cambios realizados en la colección supervisada se reflejan en la fuente de cambios de la colección.</span><span class="sxs-lookup"><span data-stu-id="80f09-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="80f09-257">**Colección de concesión:** La colección de concesión coordina el procesamiento de la fuente de cambios entre varios trabajadores.</span><span class="sxs-lookup"><span data-stu-id="80f09-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="80f09-258">Se utiliza una colección independiente para almacenar las concesiones con una concesión por partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="80f09-259">Resulta ventajoso almacenar esta colección de concesión en una cuenta diferente con la región de escritura más cerca de donde se está ejecutando el procesador de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="80f09-260">Un objeto de concesión contiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="80f09-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="80f09-261">Propietario: Especifica el host que posee la concesión.</span><span class="sxs-lookup"><span data-stu-id="80f09-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="80f09-262">Continuación: Especifica la posición (token de continuación) en la fuente de cambios para una partición determinada.</span><span class="sxs-lookup"><span data-stu-id="80f09-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="80f09-263">Marca de tiempo: Última vez que se actualizó la concesión; la marca de tiempo se puede utilizar para comprobar si la concesión se considera expirada.</span><span class="sxs-lookup"><span data-stu-id="80f09-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="80f09-264">**Host de procesador:** Cada host determina cuántas particiones se van a procesar según la cantidad de otras instancias de host que tienen concesiones activas.</span><span class="sxs-lookup"><span data-stu-id="80f09-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="80f09-265">Cuando se inicia un host, adquiere concesiones para equilibrar la carga de trabajo en todos los hosts.</span><span class="sxs-lookup"><span data-stu-id="80f09-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="80f09-266">Un host renueva periódicamente concesiones, por lo que las concesiones permanecen activas.</span><span class="sxs-lookup"><span data-stu-id="80f09-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="80f09-267">Un host establece puntos de control en el último token de continuación para su concesión para cada lectura.</span><span class="sxs-lookup"><span data-stu-id="80f09-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="80f09-268">Para garantizar la seguridad de simultaneidad, un host comprueba ETag para cada actualización de concesión.</span><span class="sxs-lookup"><span data-stu-id="80f09-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="80f09-269">También se admiten otras estrategias de puntos de control.</span><span class="sxs-lookup"><span data-stu-id="80f09-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="80f09-270">Tras el cierre, un host libera todas las concesiones pero mantiene la información de continuación, por lo que puede reanudar la lectura más adelante desde el punto de control almacenado.</span><span class="sxs-lookup"><span data-stu-id="80f09-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="80f09-271">En este momento, el número de hosts no puede ser mayor que el número de particiones (concesiones).</span><span class="sxs-lookup"><span data-stu-id="80f09-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="80f09-272">**Consumidores:** Los consumidores, o trabajadores, son subprocesos que realizan el procesamiento de fuentes de cambios iniciado por cada host.</span><span class="sxs-lookup"><span data-stu-id="80f09-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="80f09-273">Cada host de procesador puede tener varios consumidores.</span><span class="sxs-lookup"><span data-stu-id="80f09-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="80f09-274">Cada consumidor lee la fuente de cambios de la partición a la que se ha asignado y notifica a su host los cambios y las concesiones expiradas.</span><span class="sxs-lookup"><span data-stu-id="80f09-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="80f09-275">Para comprender mejor cómo funcionan estos cuatro elementos del procesador de fuente de cambios juntos, echemos un vistazo a un ejemplo en el diagrama siguiente.</span><span class="sxs-lookup"><span data-stu-id="80f09-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="80f09-276">La colección supervisada almacena documentos y utiliza "city" como la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="80f09-277">Vemos que la partición azul contiene documentos con el campo "city" de "A-e", etc.</span><span class="sxs-lookup"><span data-stu-id="80f09-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="80f09-278">Hay dos hosts, cada uno con dos consumidores, que leen las cuatro particiones en paralelo.</span><span class="sxs-lookup"><span data-stu-id="80f09-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="80f09-279">Las flechas muestran a los consumidores leyendo un punto específico de la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="80f09-280">En la primera partición, el azul más oscuro representa los cambios no leídos, mientras que el azul claro representa los cambios ya leídos de la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="80f09-281">Los hosts utilizan la colección de concesión para almacenar un valor de "continuación" para realizar un seguimiento de la posición de lectura actual para cada consumidor.</span><span class="sxs-lookup"><span data-stu-id="80f09-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Uso del host de procesador de fuente de cambios de Azure Cosmos DB](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="80f09-283">Uso de la biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="80f09-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="80f09-284">En la siguiente sección se explica cómo usar la biblioteca de procesadores de fuente de cambios en el contexto de replicación de cambios de una colección de origen a una colección de destino.</span><span class="sxs-lookup"><span data-stu-id="80f09-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="80f09-285">En este caso, la colección de origen es la colección supervisada en el procesador de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="80f09-286">**Instalación e inclusión del paquete NuGet del procesador de fuente de cambios**</span><span class="sxs-lookup"><span data-stu-id="80f09-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="80f09-287">Antes de instalar el paquete NuGet del procesador de fuente de cambios, instale primero:</span><span class="sxs-lookup"><span data-stu-id="80f09-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="80f09-288">Microsoft.Azure.DocumentDB, versión 1.13.1 o posterior</span><span class="sxs-lookup"><span data-stu-id="80f09-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="80f09-289">Newtonsoft.Json, versión 9.0.1 o una versión posterior. Instale `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e inclúyalo como una referencia.</span><span class="sxs-lookup"><span data-stu-id="80f09-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="80f09-290">**Creación una colección supervisada, de concesión y de destino** </span><span class="sxs-lookup"><span data-stu-id="80f09-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="80f09-291">Para poder usar la biblioteca de procesadores de fuente de cambios, la colección de concesión debe crearse antes de ejecutar los hosts de procesador.</span><span class="sxs-lookup"><span data-stu-id="80f09-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="80f09-292">Una vez más, es recomendable almacenar una colección de concesión en una cuenta diferente con una región de escritura más cerca de donde se está ejecutando el procesador de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="80f09-293">En este ejemplo de movimiento de datos, es necesario crear la colección de destino antes de ejecutar el host del procesador de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="80f09-294">En el código de ejemplo, llamamos a un método auxiliar para crear las colecciones supervisadas, concedidas y de destino si aún no existen.</span><span class="sxs-lookup"><span data-stu-id="80f09-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="80f09-295">Crear una colección implica precios, debido a que reserva rendimiento para que la aplicación se comunique con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="80f09-296">Para más detalles, visite la [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="80f09-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="80f09-297">*Creación de un host de procesador*</span><span class="sxs-lookup"><span data-stu-id="80f09-297">*Creating a processor host*</span></span>

<span data-ttu-id="80f09-298">La clase `ChangeFeedProcessorHost` proporciona un entorno de tiempo de ejecución seguro, seguro para subprocesos y de varios procesos para las implementaciones de procesadores de eventos que también ofrecen administración de concesión de puntos de comprobación y particiones.</span><span class="sxs-lookup"><span data-stu-id="80f09-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="80f09-299">Para usar la clase `ChangeFeedProcessorHost`, puede implementar `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="80f09-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="80f09-300">Esta interfaz contiene tres métodos:</span><span class="sxs-lookup"><span data-stu-id="80f09-300">This interface contains three methods:</span></span>

* <span data-ttu-id="80f09-301">`OpenAsync`: Esta función se llama cuando se abre el observador de la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="80f09-302">Se puede modificar para llevar a cabo una acción específica cuando se abre el consumidor u observador.</span><span class="sxs-lookup"><span data-stu-id="80f09-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="80f09-303">`CloseAsync`: Esta función se llama cuando se termina el observador de la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="80f09-304">Se puede modificar para llevar a cabo una acción específica cuando se cierra el consumidor u observador.</span><span class="sxs-lookup"><span data-stu-id="80f09-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="80f09-305">`ProcessChangesAsync`: Esta función se llama cuando hay disponibles nuevos cambios de documento en la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="80f09-306">Se puede modificar para llevar a cabo una acción específica en todas las actualizaciones de fuentes de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="80f09-307">En nuestro ejemplo, se implementa la interfaz `IChangeFeedObserver` a través de la clase `DocumentFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="80f09-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="80f09-308">En este caso, la función `ProcessChangesAsync` realiza una operación upsert (de actualización) en un documento desde la fuente de cambios en la colección de destino.</span><span class="sxs-lookup"><span data-stu-id="80f09-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="80f09-309">Este ejemplo es útil para mover datos de una colección a otra con el fin de cambiar la clave de partición de un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="80f09-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="80f09-310">*Ejecución del host de procesador*</span><span class="sxs-lookup"><span data-stu-id="80f09-310">*Running the Processor Host*</span></span>

<span data-ttu-id="80f09-311">Antes de iniciar el procesamiento de eventos, se pueden personalizar tanto las opciones de fuente de cambios como las opciones de host de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="80f09-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="80f09-312">En las tablas siguientes se resumen los campos específicos que se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="80f09-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="80f09-313">**Opciones de fuente de cambio**:</span><span class="sxs-lookup"><span data-stu-id="80f09-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="80f09-314">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="80f09-314">Property Name</span></span></th>
        <th><span data-ttu-id="80f09-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="80f09-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="80f09-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="80f09-317">Obtiene o establece el número máximo de elementos que se devolverán en la operación de enumeración en el servicio de base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="80f09-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="80f09-319">Obtiene o establece el identificador de intervalo de claves de partición para la solicitud actual en el servicio de base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="80f09-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="80f09-321">Obtiene o establece el token de continuación de solicitud en el servicio de base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="80f09-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="80f09-322">SessionToken</span></span></td>
        <td><span data-ttu-id="80f09-323">Obtiene o establece el token de sesión para su uso con coherencia de sesión en el servicio de base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="80f09-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="80f09-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="80f09-325">Obtiene o establece si la fuente de cambios del servicio de base de datos de Azure Cosmos DB debe empezar desde el principio (true) o desde la posición actual (false).</span><span class="sxs-lookup"><span data-stu-id="80f09-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="80f09-326">De forma predeterminada, se inicia desde la posición actual (false).</span><span class="sxs-lookup"><span data-stu-id="80f09-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="80f09-327">**Opciones de host de fuente de cambios**:</span><span class="sxs-lookup"><span data-stu-id="80f09-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="80f09-328">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="80f09-328">Property Name</span></span></th>
        <th><span data-ttu-id="80f09-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="80f09-329">Type</span></span></th>
        <th><span data-ttu-id="80f09-330">Descripción</span><span class="sxs-lookup"><span data-stu-id="80f09-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="80f09-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="80f09-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="80f09-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="80f09-333">Intervalo para todas las concesiones para las particiones que la instancia de ChangeFeedEventHost mantiene actualmente.</span><span class="sxs-lookup"><span data-stu-id="80f09-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="80f09-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="80f09-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="80f09-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="80f09-336">Intervalo para iniciar una tarea para calcular si las particiones se distribuyen uniformemente entre las instancias de host conocidas.</span><span class="sxs-lookup"><span data-stu-id="80f09-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="80f09-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="80f09-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="80f09-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="80f09-339">Intervalo para el que se toma la concesión en una concesión que representa una partición.</span><span class="sxs-lookup"><span data-stu-id="80f09-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="80f09-340">Si la concesión no se renueva dentro de este intervalo, expira y la propiedad de la partición se mueve a otra instancia de ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="80f09-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="80f09-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="80f09-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="80f09-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="80f09-343">Retraso entre sondeos de una partición en busca de nuevos cambios en la fuente, después de que todos los cambios actuales se purguen.</span><span class="sxs-lookup"><span data-stu-id="80f09-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="80f09-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="80f09-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="80f09-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="80f09-346">Frecuencia para establecer puntos de control en la concesión.</span><span class="sxs-lookup"><span data-stu-id="80f09-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="80f09-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="80f09-348">int</span><span class="sxs-lookup"><span data-stu-id="80f09-348">Int</span></span></td>
        <td><span data-ttu-id="80f09-349">Número mínimo de particiones para el host.</span><span class="sxs-lookup"><span data-stu-id="80f09-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="80f09-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="80f09-351">int</span><span class="sxs-lookup"><span data-stu-id="80f09-351">Int</span></span></td>
        <td><span data-ttu-id="80f09-352">Número máximo de particiones a las que el host puede dar servicio.</span><span class="sxs-lookup"><span data-stu-id="80f09-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="80f09-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="80f09-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="80f09-354">Booleano</span><span class="sxs-lookup"><span data-stu-id="80f09-354">Bool</span></span></td>
        <td><span data-ttu-id="80f09-355">Si en el inicio del host se deben eliminar o no todas las concesiones existentes y el host debe empezar desde cero.</span><span class="sxs-lookup"><span data-stu-id="80f09-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="80f09-356">Para iniciar el procesamiento de eventos, cree una instancia de `ChangeFeedProcessorHost`, proporcionando los parámetros adecuados para la colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80f09-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="80f09-357">A continuación, llame a `RegisterObserverAsync` para registrar su implementación `IChangeFeedObserver` (DocumentFeedObserver en este ejemplo) con el entorno de ejecución.</span><span class="sxs-lookup"><span data-stu-id="80f09-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="80f09-358">En este punto, el host intenta adquirir una concesión en cada intervalo de claves de partición en la colección de Azure Cosmos DB con un algoritmo "expansivo".</span><span class="sxs-lookup"><span data-stu-id="80f09-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="80f09-359">Estas concesiones duran un período de tiempo determinado y después deben renovarse.</span><span class="sxs-lookup"><span data-stu-id="80f09-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="80f09-360">A medida que nuevos nodos, instancias de trabajo en este caso, pasan a estar en línea, colocan reservas de concesión y, con el tiempo, la carga cambia entre los nodos a medida que cada host trata de adquirir más concesiones.</span><span class="sxs-lookup"><span data-stu-id="80f09-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="80f09-361">En el código de ejemplo, utilizamos una clase de fábrica (DocumentFeedObserverFactory.cs) para crear un observador y `RegistObserverFactoryAsync` para registrar dicho observador.</span><span class="sxs-lookup"><span data-stu-id="80f09-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="80f09-362">Con el tiempo, se establece un equilibrio.</span><span class="sxs-lookup"><span data-stu-id="80f09-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="80f09-363">Esta funcionalidad dinámica permite la aplicación del escalado automático basado en CPU a los consumidores para escalar y reducir verticalmente.</span><span class="sxs-lookup"><span data-stu-id="80f09-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="80f09-364">Si los cambios están disponibles en Azure Cosmos DB a una mayor velocidad de la que los consumidores pueden procesar, el aumento de la CPU en los consumidores puede usarse para producir un escalado automático en el recuento de instancias de trabajo.</span><span class="sxs-lookup"><span data-stu-id="80f09-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80f09-365">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80f09-365">Next steps</span></span>
* <span data-ttu-id="80f09-366">Pruebe los [ejemplos de código de fuente de cambios de Azure Cosmos DB incluidos en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed).</span><span class="sxs-lookup"><span data-stu-id="80f09-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="80f09-367">Introducción a la programación con los [SDK de Azure Cosmos DB](documentdb-sdk-dotnet.md) o la [API de REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="80f09-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
