---
title: 'Azure Cosmos DB: API, SDK y recursos de Java para DocumentDB | Microsoft Docs'
description: "Infórmese acerca de hello SDK como fechas de inicio, fechas de retirada y los cambios realizados entre cada versión del SDK de Java de documentos de base de datos de Azure Cosmos hello y API de Java."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="8176b-103">Azure Cosmos DB: notas de la versión y recursos del SDK de Java para DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8176b-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8176b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8176b-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="8176b-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="8176b-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="8176b-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8176b-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="8176b-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="8176b-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="8176b-108">Java</span><span class="sxs-lookup"><span data-stu-id="8176b-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="8176b-109">Python</span><span class="sxs-lookup"><span data-stu-id="8176b-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="8176b-110">REST</span><span class="sxs-lookup"><span data-stu-id="8176b-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="8176b-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="8176b-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="8176b-112">SQL</span><span class="sxs-lookup"><span data-stu-id="8176b-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="8176b-113">**Descarga del SDK**</span><span class="sxs-lookup"><span data-stu-id="8176b-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="8176b-114">Maven</span><span class="sxs-lookup"><span data-stu-id="8176b-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="8176b-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="8176b-115">**API documentation**</span></span></td><td>[<span data-ttu-id="8176b-116">Documentación de referencia de API</span><span class="sxs-lookup"><span data-stu-id="8176b-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="8176b-117">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="8176b-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="8176b-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="8176b-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="8176b-119">**Introducción**</span><span class="sxs-lookup"><span data-stu-id="8176b-119">**Get started**</span></span></td><td>[<span data-ttu-id="8176b-120">Empezar a trabajar con hello SDK de Java</span><span class="sxs-lookup"><span data-stu-id="8176b-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="8176b-121">**Tutorial de la aplicación web**</span><span class="sxs-lookup"><span data-stu-id="8176b-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="8176b-122">Desarrollo de aplicaciones web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8176b-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="8176b-123">**Tiempo de ejecución admitido actualmente**</span><span class="sxs-lookup"><span data-stu-id="8176b-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="8176b-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="8176b-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="8176b-125">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="8176b-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="8176b-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="8176b-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="8176b-127">Divide toorequest crítico correcciones de errores de procesamiento durante la partición.</span><span class="sxs-lookup"><span data-stu-id="8176b-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="8176b-128">Se ha corregido un problema con hello seguro y niveles de coherencia de BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="8176b-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="8176b-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="8176b-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="8176b-130">Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="8176b-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="8176b-131">Se ha corregido un error en la lectura de la colección en modo de sesión.</span><span class="sxs-lookup"><span data-stu-id="8176b-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="8176b-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="8176b-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="8176b-133">Habilitada compatibilidad para las colecciones particionadas con al menos 2500 RU/s y aumentos de 100 RU/s.</span><span class="sxs-lookup"><span data-stu-id="8176b-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="8176b-134">Se ha corregido un error en ensamblado nativo de hello, lo que puede producir la excepción NullRef en algunas consultas.</span><span class="sxs-lookup"><span data-stu-id="8176b-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="8176b-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="8176b-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="8176b-136">Se ha corregido un error en la configuración del motor de consulta de Hola que puede provocar excepciones para las consultas en modo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8176b-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="8176b-137">Se ha corregido algunos errores en el contenedor de la sesión de Hola que pueden provocar una excepción "Recurso de propietario no encontrado" para las solicitudes inmediatamente después de la creación de la colección.</span><span class="sxs-lookup"><span data-stu-id="8176b-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="8176b-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="8176b-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="8176b-139">Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="8176b-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="8176b-140">Consulte [Compatibilidad con agregación](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="8176b-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="8176b-141">Compatibilidad agregada para cambiar la fuente.</span><span class="sxs-lookup"><span data-stu-id="8176b-141">Added support for change feed.</span></span>
* <span data-ttu-id="8176b-142">Compatibilidad agregada para la recopilación de la información de cuota mediante RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="8176b-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="8176b-143">Compatibilidad agregada para el registro de scripts de procedimiento almacenados mediante RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="8176b-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="8176b-144">Se ha corregido un error en el que una consulta en modo DirectHttps puede bloquearse cuando se producen errores de limitación.</span><span class="sxs-lookup"><span data-stu-id="8176b-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="8176b-145">Se ha corregido un error en modo de sesión de coherencia.</span><span class="sxs-lookup"><span data-stu-id="8176b-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="8176b-146">Se ha corregido un error que puede causar una excepción NullReferenceException en HttpContext cuando la tasa de solicitudes es alta.</span><span class="sxs-lookup"><span data-stu-id="8176b-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="8176b-147">Rendimiento mejorado del modo DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="8176b-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="8176b-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="8176b-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="8176b-149">Con la API ConnectionPolicy.setProxy(), se ha agregado compatibilidad simple con proxy basada en instancias del cliente.</span><span class="sxs-lookup"><span data-stu-id="8176b-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="8176b-150">Agregado DocumentClient.close() tooproperly apagado DocumentClient instancia de la API.</span><span class="sxs-lookup"><span data-stu-id="8176b-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="8176b-151">Mejora del rendimiento en modo de conexión directa con derivando plan de consulta de Hola de ensamblados nativa de hello en lugar de hello puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8176b-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="8176b-152">Establecer FAIL_ON_UNKNOWN_PROPERTIES = false para los usuarios no necesitan toodefine JsonIgnoreProperties en su POJO.</span><span class="sxs-lookup"><span data-stu-id="8176b-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="8176b-153">Registro refactorizado toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="8176b-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="8176b-154">Se han corregido otros errores en el lector de coherencia.</span><span class="sxs-lookup"><span data-stu-id="8176b-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="8176b-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="8176b-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="8176b-156">Se corrige un error en pérdidas de conexión de hello conexión administración tooprevent en modo de conexión directa.</span><span class="sxs-lookup"><span data-stu-id="8176b-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="8176b-157">Corregido un error en la consulta TOP Hola donde pueden producir excepciones de NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="8176b-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="8176b-158">Mejorar el rendimiento reduciendo el número de Hola de llamada de red para las memorias caché interna de Hola.</span><span class="sxs-lookup"><span data-stu-id="8176b-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="8176b-159">Se ha agregado código de estado, ActivityID y la URI de la solicitud en DocumentClientException para una mejor solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="8176b-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="8176b-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="8176b-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="8176b-161">Se corrigió un problema en la administración de conexión de Hola de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="8176b-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="8176b-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="8176b-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="8176b-163">Compatibilidad agregada con el nivel de coherencia BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="8176b-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="8176b-164">Se ha agregado compatibilidad con la conectividad directa de las colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="8176b-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="8176b-165">Se ha corregido un error al realizar consultas en una base de datos con SQL.</span><span class="sxs-lookup"><span data-stu-id="8176b-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="8176b-166">Se ha corregido un error en caché de la sesión de Hola donde el token de sesión puede estar configurado incorrectamente.</span><span class="sxs-lookup"><span data-stu-id="8176b-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="8176b-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="8176b-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="8176b-168">Compatibilidad agregada con las consultas paralelas entre particiones.</span><span class="sxs-lookup"><span data-stu-id="8176b-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="8176b-169">Se ha agregado compatibilidad con las consultas TOP y ORDER BY en las colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="8176b-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="8176b-170">Compatibilidad agregada con Coherencia fuerte.</span><span class="sxs-lookup"><span data-stu-id="8176b-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="8176b-171">Se ha agregado compatibilidad con las solicitudes basadas en nombres al utilizar la conectividad directa.</span><span class="sxs-lookup"><span data-stu-id="8176b-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="8176b-172">Toomake fijo ActivityId permanezca coherente entre todos los reintentos de solicitud.</span><span class="sxs-lookup"><span data-stu-id="8176b-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="8176b-173">Se ha corregido un error relacionados con la caché de la sesión de toohello al volver a crear una colección con hello mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="8176b-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="8176b-174">Se han agregado los tipos de datos Polygon y LineString al especificar la directiva de indización de colecciones para las consultas espaciales de geovallado.</span><span class="sxs-lookup"><span data-stu-id="8176b-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="8176b-175">Problemas corregidos con Java Doc para Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="8176b-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="8176b-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="8176b-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="8176b-177">Se ha corregido un error en PartitionKeyDefinitionMap toocache colecciones de una sola partición y no hacer adicional capturar partición las solicitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="8176b-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="8176b-178">Se ha corregido un reintento de toonot de error cuando se proporciona un valor de clave de partición correcta.</span><span class="sxs-lookup"><span data-stu-id="8176b-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="8176b-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="8176b-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="8176b-180">Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.</span><span class="sxs-lookup"><span data-stu-id="8176b-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="8176b-181">Se agregó compatibilidad para el reintento automático en las solicitudes limitadas con hello de toocustomize opciones max reintentos y tiempo de espera de reintento max.</span><span class="sxs-lookup"><span data-stu-id="8176b-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="8176b-182">Consulte RetryOptions y ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="8176b-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="8176b-183">Se ha dejado de utilizar el código de creación de particiones personalizado basado en IPartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="8176b-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="8176b-184">Utilice colecciones con particiones para conseguir un almacenamiento y un rendimiento más elevados.</span><span class="sxs-lookup"><span data-stu-id="8176b-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="8176b-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="8176b-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="8176b-186">Se ha agregado compatibilidad con la directiva de reintentos de la limitación.</span><span class="sxs-lookup"><span data-stu-id="8176b-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="8176b-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="8176b-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="8176b-188">Agregar compatibilidad en tiempo de toolive (TTL) para los documentos.</span><span class="sxs-lookup"><span data-stu-id="8176b-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="8176b-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="8176b-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="8176b-190">Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8176b-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="8176b-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="8176b-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="8176b-192">Se ha corregido un error en valores de hash de HashPartitionResolver toogenerate en toobe little-endian coherente con otros SDK de.</span><span class="sxs-lookup"><span data-stu-id="8176b-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="8176b-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="8176b-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="8176b-194">Agregar Hash & intervalo tooassist de resoluciones de partición con aplicaciones de particionamiento entre varias particiones.</span><span class="sxs-lookup"><span data-stu-id="8176b-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="8176b-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="8176b-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="8176b-196">Implementación de Upsert.</span><span class="sxs-lookup"><span data-stu-id="8176b-196">Implement Upsert.</span></span> <span data-ttu-id="8176b-197">Nuevos métodos de upsertXXX agregan toosupport Upsert característica.</span><span class="sxs-lookup"><span data-stu-id="8176b-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="8176b-198">Se implementa el enrutamiento por identificador.</span><span class="sxs-lookup"><span data-stu-id="8176b-198">Implement ID Based Routing.</span></span> <span data-ttu-id="8176b-199">Sin cambios en la API pública, todos los cambios son internos.</span><span class="sxs-lookup"><span data-stu-id="8176b-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="8176b-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="8176b-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="8176b-201">Versión omitió toobring el número de versión en consonancia con el resto de SDK</span><span class="sxs-lookup"><span data-stu-id="8176b-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="8176b-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="8176b-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="8176b-203">Compatible con índice geoespacial.</span><span class="sxs-lookup"><span data-stu-id="8176b-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="8176b-204">Valida la propiedad id para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="8176b-204">Validates id property for all resources.</span></span> <span data-ttu-id="8176b-205">Los identificadores de recursos no pueden contener los caracteres ?, /, #, \, ni terminar con un espacio.</span><span class="sxs-lookup"><span data-stu-id="8176b-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="8176b-206">Agrega el nuevo encabezado "curso de transformación de índice" tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="8176b-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="8176b-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="8176b-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="8176b-208">Implementación de la directiva de indexación V2</span><span class="sxs-lookup"><span data-stu-id="8176b-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="8176b-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="8176b-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="8176b-210">SDK de GA</span><span class="sxs-lookup"><span data-stu-id="8176b-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="8176b-211">Fechas de lanzamiento y de retirada</span><span class="sxs-lookup"><span data-stu-id="8176b-211">Release & Retirement Dates</span></span>
<span data-ttu-id="8176b-212">Microsoft proporcionará la notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.</span><span class="sxs-lookup"><span data-stu-id="8176b-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="8176b-213">Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, por lo tanto, es recomendable que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="8176b-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="8176b-214">Servicio de hello rechazará cualquier base de datos con un SDK retirado tooCosmos de solicitud.</span><span class="sxs-lookup"><span data-stu-id="8176b-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="8176b-215">Todas las versiones de hello DocumentDB SDK para Java anterior tooversion **1.0.0** se retirarán en **29 de febrero de 2016**.</span><span class="sxs-lookup"><span data-stu-id="8176b-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="8176b-216">Versión</span><span class="sxs-lookup"><span data-stu-id="8176b-216">Version</span></span> | <span data-ttu-id="8176b-217">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="8176b-217">Release Date</span></span> | <span data-ttu-id="8176b-218">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="8176b-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="8176b-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="8176b-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="8176b-220">11 de julio de 2017</span><span class="sxs-lookup"><span data-stu-id="8176b-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="8176b-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="8176b-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="8176b-222">10 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="8176b-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="8176b-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="8176b-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="8176b-224">11 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="8176b-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="8176b-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="8176b-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="8176b-226">21 de febrero de 2017</span><span class="sxs-lookup"><span data-stu-id="8176b-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="8176b-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="8176b-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="8176b-228">31 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="8176b-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="8176b-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="8176b-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="8176b-230">24 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="8176b-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="8176b-232">30 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="8176b-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="8176b-234">28 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="8176b-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="8176b-236">26 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="8176b-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="8176b-238">03 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="8176b-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="8176b-240">30 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="8176b-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="8176b-242">14 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="8176b-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="8176b-244">30 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="8176b-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="8176b-246">27 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="8176b-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="8176b-248">29 de marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="8176b-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="8176b-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="8176b-250">31 de diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="8176b-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="8176b-252">04 de diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="8176b-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="8176b-254">05 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="8176b-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="8176b-256">05 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="8176b-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="8176b-258">05 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="8176b-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="8176b-260">09 de julio de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="8176b-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="8176b-262">12 de mayo de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="8176b-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8176b-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="8176b-264">07 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="8176b-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="8176b-265">0.9.5-prelease</span></span> |<span data-ttu-id="8176b-266">09 de marzo de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-266">Mar 09, 2015</span></span> |<span data-ttu-id="8176b-267">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-267">February 29, 2016</span></span> |
| <span data-ttu-id="8176b-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="8176b-268">0.9.4-prelease</span></span> |<span data-ttu-id="8176b-269">17 de febrero de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-269">February 17, 2015</span></span> |<span data-ttu-id="8176b-270">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-270">February 29, 2016</span></span> |
| <span data-ttu-id="8176b-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="8176b-271">0.9.3-prelease</span></span> |<span data-ttu-id="8176b-272">13 de enero de 2015</span><span class="sxs-lookup"><span data-stu-id="8176b-272">January 13, 2015</span></span> |<span data-ttu-id="8176b-273">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-273">February 29, 2016</span></span> |
| <span data-ttu-id="8176b-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="8176b-274">0.9.2-prelease</span></span> |<span data-ttu-id="8176b-275">19 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="8176b-275">December 19, 2014</span></span> |<span data-ttu-id="8176b-276">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-276">February 29, 2016</span></span> |
| <span data-ttu-id="8176b-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="8176b-277">0.9.1-prelease</span></span> |<span data-ttu-id="8176b-278">19 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="8176b-278">December 19, 2014</span></span> |<span data-ttu-id="8176b-279">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-279">February 29, 2016</span></span> |
| <span data-ttu-id="8176b-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="8176b-280">0.9.0-prelease</span></span> |<span data-ttu-id="8176b-281">10 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="8176b-281">December 10, 2014</span></span> |<span data-ttu-id="8176b-282">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="8176b-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="8176b-283">P+F</span><span class="sxs-lookup"><span data-stu-id="8176b-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="8176b-284">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8176b-284">See Also</span></span>
<span data-ttu-id="8176b-285">toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.</span><span class="sxs-lookup"><span data-stu-id="8176b-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

