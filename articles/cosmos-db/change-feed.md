---
title: aaaWorking con cambio de hello fuente compatibilidad en base de datos de Azure Cosmos | Documentos de Microsoft
description: "Base de datos de uso Azure Cosmos cambiar compatibilidad con fuentes tootrack cambios en documentos y realizar el procesamiento basado en eventos como desencadenadores y mantener actualizadas las cachés y análisis de sistemas."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="18ec4-104">Trabajar con compatibilidad de fuentes del cambio de hello en la base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="18ec4-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="18ec4-105">[Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos rápido y flexible, replicado globalmente, que se usa para almacenar elevados volúmenes de datos de transacciones y operaciones con una latencia predecible inferior a 10 milisegundos en lecturas y escrituras.</span><span class="sxs-lookup"><span data-stu-id="18ec4-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="18ec4-106">Esto hace que sea adecuado para IoT, juegos y aplicaciones de registro de operaciones.</span><span class="sxs-lookup"><span data-stu-id="18ec4-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="18ec4-107">Un patrón de diseño habitual en estas aplicaciones es tootrack cambios realizan tooAzure Cosmos DB datos y actualización vistas materializadas, realizan análisis en tiempo real, almacenamiento de datos toocold y generar notificaciones sobre determinados eventos en función de estos cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="18ec4-108">Hola **Cambiar fuente compatibilidad** en base de datos de Azure Cosmos permite toobuild eficaces y escalables soluciones para cada uno de estos patrones.</span><span class="sxs-lookup"><span data-stu-id="18ec4-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="18ec4-109">A cambio de fuente de soporte técnico, base de datos de Azure Cosmos proporciona una lista ordenada de documentos dentro de una colección de base de datos de Azure Cosmos en orden de hello en el que se han modificado.</span><span class="sxs-lookup"><span data-stu-id="18ec4-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="18ec4-110">Esta fuente puede ser toolisten usado para las modificaciones toodata dentro de la colección de Hola y realizar acciones tales como:</span><span class="sxs-lookup"><span data-stu-id="18ec4-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="18ec4-111">Desencadenar una tooan llamada API cuando se inserta o modifica un documento</span><span class="sxs-lookup"><span data-stu-id="18ec4-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="18ec4-112">Realizar el procesamiento en tiempo real (secuencia) sobre las actualizaciones</span><span class="sxs-lookup"><span data-stu-id="18ec4-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="18ec4-113">Sincronizar datos con una caché, un motor de búsqueda o un almacén de datos</span><span class="sxs-lookup"><span data-stu-id="18ec4-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="18ec4-114">Los cambios en Azure Cosmos DB se conservan y se pueden procesar de manera asincrónica y distribuirse entre uno o varios clientes para un procesamiento en paralelo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="18ec4-115">Echemos un vistazo a hello las API para la alimentación de cambio y cómo se pueden utilizar aplicaciones escalables en tiempo real de toobuild.</span><span class="sxs-lookup"><span data-stu-id="18ec4-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="18ec4-116">En este artículo se muestra cómo toowork con base de datos de Azure Cosmos cambiar hello API de documentos y fuente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Usar cambio de base de datos de Azure Cosmos el salto de análisis en tiempo real de toopower y escenarios informáticos orientada a eventos](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="18ec4-118">Cambiar fuente compatibilidad solo se proporciona para hello API de documentos en este momento; Hola API Graph y la API de tabla no se admiten actualmente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="18ec4-119">Casos de uso y escenarios</span><span class="sxs-lookup"><span data-stu-id="18ec4-119">Use cases and scenarios</span></span>
<span data-ttu-id="18ec4-120">Cambiar fuente permite un procesamiento eficiente de grandes conjuntos de datos con un gran volumen de escrituras y ofrece un tooidentify de conjuntos de datos completo alternativo tooquerying qué ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="18ec4-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="18ec4-121">Por ejemplo, puede realizar Hola siguiente de forma eficaz las tareas:</span><span class="sxs-lookup"><span data-stu-id="18ec4-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="18ec4-122">Actualizar una caché, un índice de búsqueda o un almacenamiento de datos con los datos almacenados en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18ec4-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="18ec4-123">Implementar niveles y el archivado de datos de nivel de aplicación, es decir, almacenar "datos activos" en la base de datos de Azure Cosmos y se reemplazan "datos inactivos" demasiado[almacenamiento de blobs de Azure](../storage/common/storage-introduction.md) o [almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18ec4-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="18ec4-124">Implementar análisis por lotes sobre los datos mediante [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="18ec4-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="18ec4-125">Implementar [canalizaciones Lambda en Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18ec4-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="18ec4-126">Azure Cosmos DB proporciona una solución de base de datos escalable que puede hacer frente tanto a la ingesta como a la consulta, e implementar arquitecturas Lambda con un bajo TCO.</span><span class="sxs-lookup"><span data-stu-id="18ec4-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="18ec4-127">Realizar cero tooanother migraciones de tiempo de inactividad de cuenta de base de datos de Azure Cosmos con un esquema de partición diferente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="18ec4-128">**Canalizaciones Lambda con Azure Cosmos DB para ingesta y consulta:**</span><span class="sxs-lookup"><span data-stu-id="18ec4-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Canalización Lambda basada en Azure Cosmos DB para ingesta y consulta](./media/change-feed/lambda.png)

<span data-ttu-id="18ec4-130">Puede usar la base de datos de Azure Cosmos tooreceive y almacenar los datos de evento de dispositivos, sensores, infraestructura y las aplicaciones y procesar estos eventos en tiempo real con [análisis de transmisiones de Azure](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), o [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18ec4-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="18ec4-131">Dentro de su [sin servidor](http://azure.com/serverless) web y aplicaciones móviles, puede seguimiento de eventos como tootrigger de perfil, preferencias o la ubicación del cliente de cambios tooyour determinadas acciones como enviar inserción dispositivos de tootheir de notificaciones mediante [Las funciones de azure](../azure-functions/functions-bindings-documentdb.md) o [servicios de aplicaciones](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="18ec4-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="18ec4-132">Si usa la base de datos de Azure Cosmos toobuild un juego, por ejemplo, puede utilizar tablas de líderes de cambio de fuente tooimplement en tiempo real en función de las puntuaciones de juegos completadas.</span><span class="sxs-lookup"><span data-stu-id="18ec4-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="18ec4-133">Funcionamiento de la fuente de cambios en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="18ec4-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="18ec4-134">Base de datos de Azure Cosmos proporciona Hola capacidad tooincrementally lee las actualizaciones realizadas tooan colección de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="18ec4-135">Esta fuente de cambio tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="18ec4-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="18ec4-136">Los cambios son persistentes en Azure Cosmos DB y pueden procesarse de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="18ec4-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="18ec4-137">Toodocuments de cambios dentro de una colección están disponibles inmediatamente en fuente de cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="18ec4-138">Cada documento tooa de cambio aparece exactamente una vez en fuente de cambio de Hola y clientes administren la lógica de puntos de comprobación.</span><span class="sxs-lookup"><span data-stu-id="18ec4-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="18ec4-139">biblioteca de fuentes del procesador de cambios de Hello proporciona semántica de puntos de comprobación automáticos y "al menos una vez".</span><span class="sxs-lookup"><span data-stu-id="18ec4-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="18ec4-140">Único cambio más reciente de Hola para un documento determinado se incluye en el registro de cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="18ec4-141">Puede que los cambios intermedios no estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="18ec4-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="18ec4-142">Hola Cambiar fuente está ordenada por orden de modificación dentro de cada valor de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="18ec4-143">No hay ningún orden garantizado entre valores de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="18ec4-144">Los cambios se pueden sincronizar desde cualquier punto en el tiempo, es decir, no hay ningún período fijo de retención de datos en el que los cambios estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="18ec4-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="18ec4-145">Los cambios están disponibles en fragmentos de intervalos de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="18ec4-146">Esta capacidad permite que los cambios de toobe de las colecciones grandes que se procesan en paralelo mediante varios consumidores/servidores.</span><span class="sxs-lookup"><span data-stu-id="18ec4-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="18ec4-147">Las aplicaciones pueden solicitar para cambiar varias fuentes de distribución simultáneamente en hello misma colección.</span><span class="sxs-lookup"><span data-stu-id="18ec4-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="18ec4-148">La fuente de cambios de Azure DB Cosmos está habilitada de forma predeterminada para todas las cuentas.</span><span class="sxs-lookup"><span data-stu-id="18ec4-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="18ec4-149">Puede usar el [rendimiento aprovisionado](request-units.md) en su región de escritura o cualquier [leer región](distribute-data-globally.md) tooread de hello Cambiar fuente, al igual que cualquier otra operación de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="18ec4-150">Hola Cambiar fuente incluye inserciones y las operaciones de actualización realizadas toodocuments dentro de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="18ec4-151">Puede capturar eliminaciones estableciendo un indicador "eliminación temporal" dentro de los documentos en lugar de eliminaciones.</span><span class="sxs-lookup"><span data-stu-id="18ec4-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="18ec4-152">Como alternativa, puede establecer un período de caducidad finita para los documentos a través de hello [capacidad TTL](time-to-live.md), por ejemplo, 24 horas y use Hola valor de esa propiedad elimina toocapture.</span><span class="sxs-lookup"><span data-stu-id="18ec4-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="18ec4-153">Con esta solución, ha cambiado de tooprocess dentro de un intervalo de tiempo más corto que el período de expiración del período de vida de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="18ec4-154">Hola Cambiar fuente está disponible para cada intervalo de claves de partición dentro de la colección de documentos de hello y, por tanto, se puede distribuir en uno o varios consumidores para el procesamiento paralelo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Procesamiento distribuido de la fuente de cambios de Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="18ec4-156">Tiene algunas opciones para implementar una fuente de cambios en el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="18ec4-157">Hola secciones inmediatamente seguimiento describen cómo tooimplement Hola fuente de cambio mediante API de REST de base de datos de Azure Cosmos Hola y Hola SDK de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18ec4-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="18ec4-158">Sin embargo, para aplicaciones. NET, recomendamos usar Hola nueva [biblioteca de procesador de fuentes de cambio](#change-feed-processor) para procesar eventos de hello cambian fuente ya que simplifica los cambios de lectura en particiones y permite que varios subprocesos que se trabaja en paralelo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="18ec4-159"><a id="rest-apis"></a>Trabajar con hello REST API y SDK de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="18ec4-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="18ec4-160">Azure Cosmos DB proporciona contenedores elásticos de almacenamiento y rendimiento denominados **colecciones**.</span><span class="sxs-lookup"><span data-stu-id="18ec4-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="18ec4-161">Los datos dentro de las colecciones están agrupados de manera lógica mediante [claves de partición](partition-data.md) para mejorar la escalabilidad y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="18ec4-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="18ec4-162">Azure Cosmos DB proporciona varias API para acceder a estos datos, entre las que se incluyen búsqueda por identificador (leer/obtener), consulta y fuentes de lectura (exámenes).</span><span class="sxs-lookup"><span data-stu-id="18ec4-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="18ec4-163">Hello Cambiar fuente puede obtenerse rellenando dos toohello de encabezados de solicitud nuevos documentos `ReadDocumentFeed` API y se pueden procesar en paralelo en intervalos de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="18ec4-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="18ec4-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="18ec4-165">Examinemos brevemente cómo funciona ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="18ec4-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="18ec4-166">Base de datos de Azure Cosmos admite la lectura de una fuente de documentos dentro de una colección a través de hello `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="18ec4-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="18ec4-167">Por ejemplo, hello solicitud siguiente devuelve una página de documentos dentro de hello `serverlogs` colección.</span><span class="sxs-lookup"><span data-stu-id="18ec4-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="18ec4-168">Pueden estar limitados resultados mediante el uso de hello `x-ms-max-item-count` encabezado y las lecturas se pueden reanudar para volver a enviar la solicitud de hello con un `x-ms-continuation` encabezado se devuelve en la respuesta anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="18ec4-169">Cuando se realiza desde un único cliente, `ReadDocumentFeed` realiza la iteración de los resultados entre particiones en serie.</span><span class="sxs-lookup"><span data-stu-id="18ec4-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="18ec4-170">**Fuente de documento de lectura en serie**</span><span class="sxs-lookup"><span data-stu-id="18ec4-170">**Serial read document feed**</span></span>

<span data-ttu-id="18ec4-171">También puede recuperar fuente hello de documentos mediante uno de hello admitida [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="18ec4-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="18ec4-172">Por ejemplo, hello fragmento siguiente muestra cómo hello toouse [ReadDocumentFeedAsync método](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) en. NET.</span><span class="sxs-lookup"><span data-stu-id="18ec4-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="18ec4-173">Ejecución distribuida del ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="18ec4-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="18ec4-174">En el caso de colecciones que contienen terabytes de datos o mayores, o que realizan la ingesta de grandes volúmenes de actualizaciones, la ejecución en serie de la fuente de lectura desde una única máquina cliente puede que no sea una solución práctica.</span><span class="sxs-lookup"><span data-stu-id="18ec4-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="18ec4-175">En orden toosupport estos escenarios de grandes cantidades de datos, base de datos de Azure Cosmos proporciona las API toodistribute `ReadDocumentFeed` llamadas de forma transparente a través de varios lectores/consumidores de cliente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="18ec4-176">**Fuente de documentos de lectura distribuida**</span><span class="sxs-lookup"><span data-stu-id="18ec4-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="18ec4-177">tooprovide escalables de procesamiento de cambios incrementales, Azure Cosmos DB admite un modelo de escalabilidad horizontal de cambio de hello fuente API basada en rangos de las claves de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="18ec4-178">Puede obtener una lista de intervalos de claves de partición para una colección mediante la ejecución de una llamada a `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="18ec4-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="18ec4-179">Para cada intervalo de claves de partición, puede realizar un `ReadDocumentFeed` tooread documentos con las claves de partición dentro de ese intervalo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="18ec4-180">Recuperación de los intervalos de claves de partición para una colección</span><span class="sxs-lookup"><span data-stu-id="18ec4-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="18ec4-181">Puede recuperar los intervalos de clave de partición de Hola Hola solicitante `pkranges` recursos dentro de una colección.</span><span class="sxs-lookup"><span data-stu-id="18ec4-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="18ec4-182">Por ejemplo hello siguiente solicitud recupera Hola lista de intervalos de clave de partición para hello `serverlogs` colección:</span><span class="sxs-lookup"><span data-stu-id="18ec4-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="18ec4-183">Esta solicitud devuelve Hola después de respuesta que contiene metadatos sobre los intervalos de clave de partición de hello:</span><span class="sxs-lookup"><span data-stu-id="18ec4-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="18ec4-184">**Propiedades de intervalo de claves de partición**: cada intervalo de claves de partición incluye propiedades de metadatos de hello en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="18ec4-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="18ec4-185">Nombre de encabezado</span><span class="sxs-lookup"><span data-stu-id="18ec4-185">Header name</span></span></th>
        <th><span data-ttu-id="18ec4-186">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ec4-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-187">id</span><span class="sxs-lookup"><span data-stu-id="18ec4-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="18ec4-188">Id. de Hello para el intervalo de claves de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="18ec4-189">Se trata de un identificador estable y único dentro de cada colección.</span><span class="sxs-lookup"><span data-stu-id="18ec4-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="18ec4-190">Debe utilizarse en hello después llamada tooread cambios por intervalo de claves de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="18ec4-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="18ec4-192">valor de hash de clave de Hello máximo de las particiones de intervalo de claves de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="18ec4-193">Solo para uso interno.</span><span class="sxs-lookup"><span data-stu-id="18ec4-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="18ec4-194">minInclusive</span></span></td>
        <td><span data-ttu-id="18ec4-195">valor de hash de clave de Hello mínimo de la partición de intervalo de claves de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="18ec4-196">Solo para uso interno.</span><span class="sxs-lookup"><span data-stu-id="18ec4-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="18ec4-197">Puede hacerlo mediante uno de hello admitida [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="18ec4-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="18ec4-198">Por ejemplo, hello fragmento de código siguiente muestra cómo intervalos de clave de partición tooretrieve en .NET mediante hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) método.</span><span class="sxs-lookup"><span data-stu-id="18ec4-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="18ec4-199">Base de datos de Azure Cosmos admite la recuperación de documentos por intervalo de claves de partición por hello configuración opcional `x-ms-documentdb-partitionkeyrangeid` encabezado.</span><span class="sxs-lookup"><span data-stu-id="18ec4-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="18ec4-200">Realización de una operación ReadDocumentFeed incremental</span><span class="sxs-lookup"><span data-stu-id="18ec4-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="18ec4-201">ReadDocumentFeed admite Hola siguiente escenarios y las tareas para el procesamiento incremental de cambios en las colecciones de base de datos de Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="18ec4-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="18ec4-202">Lectura de todos los cambios toodocuments desde el principio de hello, es decir, de creación de la colección.</span><span class="sxs-lookup"><span data-stu-id="18ec4-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="18ec4-203">Lectura de todos los cambios toofuture actualizaciones toodocuments de hora actual, o bien los cambios desde un tiempo especificado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="18ec4-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="18ec4-204">Leer toodocuments de todos los cambios de una versión lógica de colección de hello (ETag).</span><span class="sxs-lookup"><span data-stu-id="18ec4-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="18ec4-205">Puede que los consumidores según Hola procedente de las solicitudes de lectura fuente incrementales la ETag de punto de comprobación.</span><span class="sxs-lookup"><span data-stu-id="18ec4-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="18ec4-206">los cambios de Hello incluyen toodocuments inserciones y actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="18ec4-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="18ec4-207">elimina toocapture, debe usar una propiedad de "eliminación temporal" dentro de los documentos o usar hello [propiedad TTL integrada](time-to-live.md) toosignal una eliminación pendiente en hello Cambiar fuente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="18ec4-208">Hola siguientes Hola de listas de tabla [solicitud](/rest/api/documentdb/common-documentdb-rest-request-headers.md) y [encabezados de respuesta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para las operaciones de ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="18ec4-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="18ec4-209">**Encabezados de solicitud para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="18ec4-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="18ec4-210">Nombre de encabezado</span><span class="sxs-lookup"><span data-stu-id="18ec4-210">Header name</span></span></th>
        <th><span data-ttu-id="18ec4-211">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ec4-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="18ec4-212">A-IM</span></span></td>
        <td><span data-ttu-id="18ec4-213">Debe establecerse demasiado "Incremental fuente de distribución", o se omite en caso contrario</span><span class="sxs-lookup"><span data-stu-id="18ec4-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="18ec4-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="18ec4-215">Ningún encabezado: devuelve todos los cambios de hello partir (creación de la colección)</span><span class="sxs-lookup"><span data-stu-id="18ec4-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="18ec4-216">"*": devuelve todos los nuevos toodata cambios dentro de la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="18ec4-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="18ec4-217">&lt;ETag&gt;: si establece tooa colección ETag, devuelve todos los cambios realizados desde esa marca de tiempo lógico</span><span class="sxs-lookup"><span data-stu-id="18ec4-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="18ec4-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="18ec4-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="18ec4-219">Formato de hora RFC 1123; se omite si se especifica If-None-Match</span><span class="sxs-lookup"><span data-stu-id="18ec4-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="18ec4-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="18ec4-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="18ec4-221">Hola el identificador del intervalo de claves de partición para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="18ec4-222">**Encabezados de respuesta para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="18ec4-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="18ec4-223">Nombre de encabezado</span><span class="sxs-lookup"><span data-stu-id="18ec4-223">Header name</span></span></th>
        <th><span data-ttu-id="18ec4-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ec4-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-225">ETag</span><span class="sxs-lookup"><span data-stu-id="18ec4-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="18ec4-226">número de secuencia lógica de Hello (LSN) del último documento devuelto en respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="18ec4-227">La operación ReadDocumentFeed incremental se puede reanudar reenviando este valor en If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="18ec4-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="18ec4-228">Este es un tooreturn de solicitud de ejemplo todos los cambios incrementales en la colección de versión/ETag lógico hello `28535` y rangos con clave de partición = `16`:</span><span class="sxs-lookup"><span data-stu-id="18ec4-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="18ec4-229">Cambios se ordenan por tiempo dentro de cada valor de clave de partición dentro de intervalo de claves de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="18ec4-230">No hay ningún orden garantizado entre valores de clave de partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="18ec4-231">Si no hay más resultados que pueden caber en una sola página, puede leer la siguiente página de resultados de Hola para volver a enviar la solicitud de hello con hello `If-None-Match` encabezado con valor igual toohello `etag` de respuesta de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="18ec4-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="18ec4-232">Si varios documentos fueron insertadas o actualizadas transaccionalmente dentro de un procedimiento almacenado o desencadenador, todos se devolverá en hello mismo página de respuesta.</span><span class="sxs-lookup"><span data-stu-id="18ec4-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="18ec4-233">A cambio de fuente, podría obtener más elementos devueltos en una página que los especificados en `x-ms-max-item-count` en caso de hello de varios documentos insertados o actualizados en los procedimientos almacenados o desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="18ec4-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="18ec4-234">Al utilizar Hola .NET SDK (1.17.0), establezca el campo de hello `StartTime` en `ChangeFeedOptions` toodirectly devuelto cambiado documentos desde `StartTime` al llamar a `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="18ec4-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="18ec4-235">Mediante la especificación de `If-Modified-Since` con hello API de REST, la solicitud devolverá no Hola documentos por sí mismos, pero en su lugar el token de continuación Hola o `etag` en el encabezado de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="18ec4-236">documentos de hello tooreturn Hola modificado especificado tiempo, token de continuación hello `etag` , a continuación, debe usarse en la siguiente solicitud de hello con `If-None-Match` tooreturn Hola documentos en cuestión.</span><span class="sxs-lookup"><span data-stu-id="18ec4-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="18ec4-237">Hola .NET SDK proporciona hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) y [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess realizados tooa colección de las clases auxiliares.</span><span class="sxs-lookup"><span data-stu-id="18ec4-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="18ec4-238">Hello fragmento de código siguiente muestra cómo tooretrieve todos los cambios desde principio hello mediante Hola .NET SDK desde un solo cliente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="18ec4-239">Y hello fragmento de código siguiente muestra cómo tooprocess cambia en tiempo real con la base de datos de Azure Cosmos mediante cambios de hello fuente soporte técnico y Hola delante de la función.</span><span class="sxs-lookup"><span data-stu-id="18ec4-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="18ec4-240">Hola primera llamada devuelve todos los documentos de hello en la colección de Hola y Hola en segundo lugar solo devuelve Hola dos documentos creados que se crearon desde el último punto de comprobación Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="18ec4-241">También puede filtrar la fuente de cambio de hello mediante lógica tooselectively proceso eventos de cliente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="18ec4-242">Por ejemplo, este es un fragmento de código que usa tooprocess LINQ de lado de cliente solo los eventos de cambio de temperatura de sensores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="18ec4-243"><a id="change-feed-processor"></a>Biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="18ec4-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="18ec4-244">Otra opción es hello toouse [biblioteca DB Cosmos Azure Cambiar fuente procesador](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que puede ayudar a distribuir fácilmente el procesamiento de un cambio de fuente de distribución a través de varios consumidores de eventos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="18ec4-245">biblioteca de Hello es excelente para la creación de cambio de los lectores de fuentes de distribución en la plataforma .NET de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="18ec4-246">Algunos flujos de trabajo que se simplifica mediante el uso de biblioteca de fuente de distribución de procesador de cambios de Hola a través de métodos de hello incluidos en hello otros SDK de base de datos de Cosmos incluyen:</span><span class="sxs-lookup"><span data-stu-id="18ec4-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="18ec4-247">Extracción de actualizaciones de fuente de cambios cuando los datos se almacenan en varias particiones</span><span class="sxs-lookup"><span data-stu-id="18ec4-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="18ec4-248">Mover o replicar datos de una colección tooanother</span><span class="sxs-lookup"><span data-stu-id="18ec4-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="18ec4-249">Ejecución en paralelo de las acciones desencadenadas por toodata de actualizaciones y cambio de fuente</span><span class="sxs-lookup"><span data-stu-id="18ec4-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="18ec4-250">Aunque utilizando Hola API Hola Cosmos SDK proporciona acceso preciso toochange fuente de distribución de actualizaciones en cada partición, el uso de biblioteca de fuente de distribución de procesador de cambios de hello simplifica cambios de lectura a través de las particiones y varios subprocesos funcionan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="18ec4-251">En lugar de leer manualmente los cambios de cada contenedor y guardar un token de continuación para cada partición, Hola Cambiar fuente procesador administra automáticamente los cambios de lectura a través de las particiones que usan un mecanismo de concesión.</span><span class="sxs-lookup"><span data-stu-id="18ec4-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="18ec4-252">biblioteca de Hello está disponible como un paquete de NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) y desde el código de origen como un Github [ejemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="18ec4-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="18ec4-253">Descripción de la biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="18ec4-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="18ec4-254">Hay cuatro componentes principales de la implementación de hello Cambiar fuente procesador: Hola supervisa la colección, la recopilación de concesión de hello, host de procesador de Hola y los consumidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="18ec4-255">**Recopilación supervisada:** colección Hola supervisado es datos de Hola desde qué Hola se genera el cambio de fuente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="18ec4-256">Cualquier recopilación de toohello supervisando las inserciones y cambios se reflejan en la fuente de cambio de Hola de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="18ec4-257">**Colección de concesión:** Hola coordenadas de la colección de concesión procesar cambio Hola fuente entre varios trabajadores.</span><span class="sxs-lookup"><span data-stu-id="18ec4-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="18ec4-258">Una colección independiente es toostore usado Hola concesiones con una concesión por partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="18ec4-259">Resulta ventajoso toostore esta colección de concesión en otra cuenta con hello escribir Hola región de toowhere cuanto más se acerque el procesador de fuente de cambio está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="18ec4-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="18ec4-260">Un objeto de concesión contiene Hola siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="18ec4-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="18ec4-261">Propietario: Especifica el host de Hola que posee la concesión de Hola</span><span class="sxs-lookup"><span data-stu-id="18ec4-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="18ec4-262">Continuación: Especifica la posición de hello (token de continuación) en fuentes de distribución para una partición determinada, cambie Hola</span><span class="sxs-lookup"><span data-stu-id="18ec4-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="18ec4-263">Marca de tiempo: Última vez que se actualizó la concesión; marca de tiempo de Hello puede ser toocheck usado si concesión Hola se considera caducado</span><span class="sxs-lookup"><span data-stu-id="18ec4-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="18ec4-264">**Host de procesador:** cada host determina cuántos tooprocess particiones según el número de instancias de hosts tengan concesiones activas.</span><span class="sxs-lookup"><span data-stu-id="18ec4-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="18ec4-265">Cuando se inicia un host, adquiere la carga de trabajo de concesiones toobalance hello en todos los hosts.</span><span class="sxs-lookup"><span data-stu-id="18ec4-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="18ec4-266">Un host renueva periódicamente concesiones, por lo que las concesiones permanecen activas.</span><span class="sxs-lookup"><span data-stu-id="18ec4-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="18ec4-267">Una host puntos de control hello última continuación tooits token concesión para cada lectura.</span><span class="sxs-lookup"><span data-stu-id="18ec4-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="18ec4-268">comprobaciones de un host de seguridad de simultaneidad tooensure, hello ETag para cada actualización de la concesión.</span><span class="sxs-lookup"><span data-stu-id="18ec4-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="18ec4-269">También se admiten otras estrategias de puntos de control.</span><span class="sxs-lookup"><span data-stu-id="18ec4-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="18ec4-270">Tras el cierre, un host libera todas las concesiones pero mantiene Hola información de continuación, por lo que puede reanudar la lectura desde el punto de comprobación almacenado Hola más adelante.</span><span class="sxs-lookup"><span data-stu-id="18ec4-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="18ec4-271">En este momento el número de Hola de hosts no puede ser mayor que el número de Hola de particiones (concesiones).</span><span class="sxs-lookup"><span data-stu-id="18ec4-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="18ec4-272">**Los consumidores:** consumidores o los trabajadores, son los subprocesos que realizan cambios Hola fuente procesamiento iniciado por cada host.</span><span class="sxs-lookup"><span data-stu-id="18ec4-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="18ec4-273">Cada host de procesador puede tener varios consumidores.</span><span class="sxs-lookup"><span data-stu-id="18ec4-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="18ec4-274">Cada consumidor lee Hola Cambiar fuente de hello partición se asigna tooand notifica a su host de cambios y expirado concesiones.</span><span class="sxs-lookup"><span data-stu-id="18ec4-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="18ec4-275">toofurther comprender cómo funcionan conjuntamente estos cuatro elementos de procesador de fuente de cambios, echemos un vistazo a un ejemplo de Hola siguiente diagrama.</span><span class="sxs-lookup"><span data-stu-id="18ec4-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="18ec4-276">Hola supervisa colección almacena los documentos y utiliza Hola "city" como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="18ec4-277">Vemos que partición Hola azul contiene documentos con el campo "city" hello "A-e" y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="18ec4-278">Hay dos hosts, cada uno con dos consumidores leyendo de particiones de hello cuatro en paralelo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="18ec4-279">las flechas de Hello muestran los consumidores de hello leer desde un punto específico en hello Cambiar fuente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="18ec4-280">En la primera partición hello, azul de hello borde más oscuro representa los cambios no leídos mientras azul claro Hola representa Hola ya leer los cambios en la fuente de cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="18ec4-281">los hosts de Hello usan Hola concesión colección toostore una pista de tookeep del valor de "continuación" de hello actual de lectura de posición para cada consumidor.</span><span class="sxs-lookup"><span data-stu-id="18ec4-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Cambio de la base de datos de Azure Cosmos de Hola de usar el salto de host de procesador](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="18ec4-283">Uso de la biblioteca de procesadores de fuente de cambios</span><span class="sxs-lookup"><span data-stu-id="18ec4-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="18ec4-284">Hola siguiente sección explica cómo toouse Hola biblioteca de procesador de fuente de cambios en el contexto de Hola de replicación de cambios de una colección de destino de tooa de colección de origen.</span><span class="sxs-lookup"><span data-stu-id="18ec4-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="18ec4-285">En este caso, Hola origen colección está Hola supervisado en el procesador de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="18ec4-286">**Instalar e incluyen el paquete de NuGet del procesador de fuente de cambio de Hola**</span><span class="sxs-lookup"><span data-stu-id="18ec4-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="18ec4-287">Antes de instalar el paquete NuGet del procesador de fuente de cambios, instale primero:</span><span class="sxs-lookup"><span data-stu-id="18ec4-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="18ec4-288">Microsoft.Azure.DocumentDB, versión 1.13.1 o posterior</span><span class="sxs-lookup"><span data-stu-id="18ec4-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="18ec4-289">Newtonsoft.Json, versión 9.0.1 o una versión posterior. Instale `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e inclúyalo como una referencia.</span><span class="sxs-lookup"><span data-stu-id="18ec4-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="18ec4-290">**Creación una colección supervisada, de concesión y de destino** </span><span class="sxs-lookup"><span data-stu-id="18ec4-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="18ec4-291">Hola de orden toouse biblioteca de procesador de cambios de fuente, colección de concesión de hello debe toobe creado antes de ejecutar hosts de procesador de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="18ec4-292">Una vez más, es recomendable que almacene una colección de concesión en otra cuenta con un hello más cerca de toowhere de escritura región que está ejecutando el procesador de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="18ec4-293">En este ejemplo de movimiento de datos, necesitamos recopilación de destino de hello toocreate antes de ejecutar el host de procesador de fuente de cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="18ec4-294">En el código de ejemplo de Hola llamamos un Hola de toocreate del método auxiliar supervisado, concedidas por y las colecciones de destino si aún no existen.</span><span class="sxs-lookup"><span data-stu-id="18ec4-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="18ec4-295">Crear una colección tiene precios implicaciones, tal y como está reservando para hello toocommunicate de aplicación con la base de datos de Azure Cosmos rendimiento.</span><span class="sxs-lookup"><span data-stu-id="18ec4-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="18ec4-296">Para obtener más detalles, visite hello [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="18ec4-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="18ec4-297">*Creación de un host de procesador*</span><span class="sxs-lookup"><span data-stu-id="18ec4-297">*Creating a processor host*</span></span>

<span data-ttu-id="18ec4-298">Hola `ChangeFeedProcessorHost` clase proporciona un entorno en tiempo de ejecución de subprocesos, varios procesos y segura para las implementaciones de procesador de eventos que también proporciona administración de concesión de puntos de comprobación y la partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="18ec4-299">Hola toouse `ChangeFeedProcessorHost` (clase), puede implementar `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="18ec4-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="18ec4-300">Esta interfaz contiene tres métodos:</span><span class="sxs-lookup"><span data-stu-id="18ec4-300">This interface contains three methods:</span></span>

* <span data-ttu-id="18ec4-301">`OpenAsync`: Esta función se llama cuando se abre el observador de la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="18ec4-302">Puede ser modificado tooperform una acción específica cuando se abre el consumidor/observador.</span><span class="sxs-lookup"><span data-stu-id="18ec4-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="18ec4-303">`CloseAsync`: Esta función se llama cuando se termina el observador de la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="18ec4-304">Puede ser modificado tooperform una acción específica cuando se cierra el consumidor/observador.</span><span class="sxs-lookup"><span data-stu-id="18ec4-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="18ec4-305">`ProcessChangesAsync`: Esta función se llama cuando hay disponibles nuevos cambios de documento en la fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="18ec4-306">Puede ser modificado tooperform una acción específica en todas las actualizaciones de cambio de fuente.</span><span class="sxs-lookup"><span data-stu-id="18ec4-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="18ec4-307">En nuestro ejemplo, implementamos interfaz hello `IChangeFeedObserver` a través de hello `DocumentFeedObserver` clase.</span><span class="sxs-lookup"><span data-stu-id="18ec4-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="18ec4-308">En este caso, Hola `ProcessChangesAsync` función upserts (actualizaciones de) un documento de cambio de fuente en la colección de destino Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="18ec4-309">En este ejemplo es útil para mover datos de una colección tooanother en clave de partición de orden toochange Hola de un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="18ec4-310">*Hola ejecución procesador de Host*</span><span class="sxs-lookup"><span data-stu-id="18ec4-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="18ec4-311">Antes de iniciar el procesamiento de eventos, se pueden personalizar tanto las opciones de fuente de cambios como las opciones de host de fuente de cambios.</span><span class="sxs-lookup"><span data-stu-id="18ec4-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="18ec4-312">en hello las tablas siguientes se resumen los campos específicos de Hola que se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="18ec4-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="18ec4-313">**Opciones de fuente de cambio**:</span><span class="sxs-lookup"><span data-stu-id="18ec4-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="18ec4-314">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="18ec4-314">Property Name</span></span></th>
        <th><span data-ttu-id="18ec4-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ec4-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="18ec4-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="18ec4-317">Obtiene o establece el número máximo de Hola de toobe de elementos devuelto en la operación de enumeración de hello en el servicio de base de datos de la base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="18ec4-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="18ec4-319">Obtiene o establece el Id. del intervalo de claves de partición de hello para la solicitud actual de hello en el servicio de base de datos de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="18ec4-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="18ec4-321">Obtiene o establece el token de continuación de solicitud de hello en el servicio de base de datos de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="18ec4-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="18ec4-322">SessionToken</span></span></td>
        <td><span data-ttu-id="18ec4-323">Obtiene o establece el token de sesión de Hola para su uso con coherencia de la sesión en el servicio de base de datos de la base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="18ec4-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="18ec4-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="18ec4-325">Obtiene o establece si el cambio de la fuente en el servicio de base de datos de base de datos de Azure Cosmos Hola debe iniciar desde Hola partir (true) o actual (false).</span><span class="sxs-lookup"><span data-stu-id="18ec4-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="18ec4-326">De forma predeterminada, se inicia desde la posición actual (false).</span><span class="sxs-lookup"><span data-stu-id="18ec4-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="18ec4-327">**Opciones de host de fuente de cambios**:</span><span class="sxs-lookup"><span data-stu-id="18ec4-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="18ec4-328">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="18ec4-328">Property Name</span></span></th>
        <th><span data-ttu-id="18ec4-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="18ec4-329">Type</span></span></th>
        <th><span data-ttu-id="18ec4-330">Descripción</span><span class="sxs-lookup"><span data-stu-id="18ec4-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="18ec4-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="18ec4-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18ec4-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="18ec4-333">intervalo de saludo para todas las concesiones para las particiones que actualmente mantenidos por la instancia de ChangeFeedEventHost Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="18ec4-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="18ec4-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18ec4-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="18ec4-336">Hola tookick intervalo desactivar un toocompute tarea si las particiones se distribuyen uniformemente entre las instancias de host conocidos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="18ec4-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="18ec4-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18ec4-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="18ec4-339">intervalo de saludo para qué Hola concesión se usa en una concesión que representa una partición.</span><span class="sxs-lookup"><span data-stu-id="18ec4-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="18ec4-340">Si no se renueva la concesión de hello dentro de este intervalo, ha expirado y propiedad de partición de hello pasa tooanother ChangeFeedEventHost instancia.</span><span class="sxs-lookup"><span data-stu-id="18ec4-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="18ec4-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="18ec4-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="18ec4-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="18ec4-343">fuente de retraso de Hello entre el sondeo de una partición para los nuevos cambios en hello, después de que se agotan todos los cambios actuales.</span><span class="sxs-lookup"><span data-stu-id="18ec4-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="18ec4-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="18ec4-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="18ec4-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="18ec4-346">Hola concesiones de toocheckpoint de frecuencia.</span><span class="sxs-lookup"><span data-stu-id="18ec4-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="18ec4-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="18ec4-348">int</span><span class="sxs-lookup"><span data-stu-id="18ec4-348">Int</span></span></td>
        <td><span data-ttu-id="18ec4-349">Recuento mínimo de la partición de Hello para el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="18ec4-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="18ec4-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="18ec4-351">int</span><span class="sxs-lookup"><span data-stu-id="18ec4-351">Int</span></span></td>
        <td><span data-ttu-id="18ec4-352">número máximo de Hola de host de Hola de particiones puede servir.</span><span class="sxs-lookup"><span data-stu-id="18ec4-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="18ec4-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="18ec4-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="18ec4-354">Booleano</span><span class="sxs-lookup"><span data-stu-id="18ec4-354">Bool</span></span></td>
        <td><span data-ttu-id="18ec4-355">Si en hello inicio del host de hello todas las concesiones existentes debe eliminarse y host de hello debe empezar desde cero.</span><span class="sxs-lookup"><span data-stu-id="18ec4-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="18ec4-356">crear una instancia de toostart procesamiento de eventos, `ChangeFeedProcessorHost`, proporcionando los parámetros apropiados de hello para la colección de la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18ec4-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="18ec4-357">A continuación, llame a `RegisterObserverAsync` tooregister su `IChangeFeedObserver` implementación (DocumentFeedObserver en este ejemplo) con hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="18ec4-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="18ec4-358">En este momento, el host de hello intente tooacquire una concesión en cada intervalo de claves de partición en la colección de base de datos de Azure Cosmos Hola usando un algoritmo "expansivo".</span><span class="sxs-lookup"><span data-stu-id="18ec4-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="18ec4-359">Estas concesiones duran un período de tiempo determinado y después deben renovarse.</span><span class="sxs-lookup"><span data-stu-id="18ec4-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="18ec4-360">Como nuevos nodos, instancias de trabajo, en este caso, se ponen en línea, colocan reservas de concesiones y con el tiempo carga Hola se desplaza entre los nodos como los intentos de cada host tooacquire más concesiones.</span><span class="sxs-lookup"><span data-stu-id="18ec4-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="18ec4-361">En el código de ejemplo de Hola, usamos un toocreate (DocumentFeedObserverFactory.cs) de la clase de generador un observador y hello `RegistObserverFactoryAsync` observador de hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="18ec4-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="18ec4-362">Con el tiempo, se establece un equilibrio.</span><span class="sxs-lookup"><span data-stu-id="18ec4-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="18ec4-363">Esta capacidad dinámica permite basada en CPU tooconsumers toobe aplica la escala automática de ampliación y reducción.</span><span class="sxs-lookup"><span data-stu-id="18ec4-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="18ec4-364">Si los cambios están disponibles en la base de datos de Azure Cosmos en mayor velocidad que los consumidores pueden procesar, aumento de la CPU de hello en los consumidores puede ser usado toocause una escala automática en el recuento de instancias de trabajo.</span><span class="sxs-lookup"><span data-stu-id="18ec4-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18ec4-365">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18ec4-365">Next steps</span></span>
* <span data-ttu-id="18ec4-366">Intente hello [cambio de base de datos de Azure Cosmos fuente ejemplos de código en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="18ec4-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="18ec4-367">Comenzar a codificar con hello [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="18ec4-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
