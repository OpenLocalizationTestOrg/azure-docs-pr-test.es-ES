---
title: 'Azure Cosmos DB: API, SDK y recursos de Java para DocumentDB | Microsoft Docs'
description: "Obtenga toda la información sobre la API y el SDK de Java incluidas la fechas de lanzamiento, fechas de retirada y cambios realizados entre las versiones del SDK de Java para DocumentDB de Azure Cosmos DB."
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
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="d8b08-103">Azure Cosmos DB: notas de la versión y recursos del SDK de Java para DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d8b08-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8b08-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d8b08-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="d8b08-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="d8b08-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="d8b08-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d8b08-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="d8b08-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="d8b08-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="d8b08-108">Java</span><span class="sxs-lookup"><span data-stu-id="d8b08-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="d8b08-109">Python</span><span class="sxs-lookup"><span data-stu-id="d8b08-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="d8b08-110">REST</span><span class="sxs-lookup"><span data-stu-id="d8b08-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="d8b08-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="d8b08-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="d8b08-112">SQL</span><span class="sxs-lookup"><span data-stu-id="d8b08-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="d8b08-113">**Descarga del SDK**</span><span class="sxs-lookup"><span data-stu-id="d8b08-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="d8b08-114">Maven</span><span class="sxs-lookup"><span data-stu-id="d8b08-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="d8b08-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="d8b08-115">**API documentation**</span></span></td><td>[<span data-ttu-id="d8b08-116">Documentación de referencia de API</span><span class="sxs-lookup"><span data-stu-id="d8b08-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="d8b08-117">**Contribuya al SDK**</span><span class="sxs-lookup"><span data-stu-id="d8b08-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="d8b08-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="d8b08-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="d8b08-119">**Primeros pasos**</span><span class="sxs-lookup"><span data-stu-id="d8b08-119">**Get started**</span></span></td><td>[<span data-ttu-id="d8b08-120">Introducción al SDK de Java</span><span class="sxs-lookup"><span data-stu-id="d8b08-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="d8b08-121">**Tutorial de la aplicación web**</span><span class="sxs-lookup"><span data-stu-id="d8b08-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="d8b08-122">Desarrollo de aplicaciones web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d8b08-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="d8b08-123">**Tiempo de ejecución admitido actualmente**</span><span class="sxs-lookup"><span data-stu-id="d8b08-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="d8b08-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="d8b08-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="d8b08-125">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="d8b08-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="d8b08-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="d8b08-127">Correcciones de errores críticos solicitará el procesamiento durante la división en particiones.</span><span class="sxs-lookup"><span data-stu-id="d8b08-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="d8b08-128">Se ha corregido un problema con los niveles de coherencia seguro y BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="d8b08-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="d8b08-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="d8b08-130">Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="d8b08-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="d8b08-131">Se ha corregido un error en la lectura de la colección en modo de sesión.</span><span class="sxs-lookup"><span data-stu-id="d8b08-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="d8b08-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="d8b08-133">Habilitada compatibilidad para las colecciones particionadas con al menos 2500 RU/s y aumentos de 100 RU/s.</span><span class="sxs-lookup"><span data-stu-id="d8b08-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="d8b08-134">Se ha corregido un error en el ensamblado nativo que puede dar lugar a la excepción NullRef en algunas consultas.</span><span class="sxs-lookup"><span data-stu-id="d8b08-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="d8b08-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="d8b08-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="d8b08-136">Se ha corregido un error en la configuración del motor de consulta que puede provocar excepciones para las consultas en modo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d8b08-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="d8b08-137">Se han corregido algunos errores en el contenedor de sesiones que pueden provocar una excepción "Recurso de propietario no encontrado" para las solicitudes inmediatamente después de la creación de la colección.</span><span class="sxs-lookup"><span data-stu-id="d8b08-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="d8b08-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="d8b08-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="d8b08-139">Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="d8b08-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="d8b08-140">Consulte [Compatibilidad con agregación](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="d8b08-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="d8b08-141">Compatibilidad agregada para cambiar la fuente.</span><span class="sxs-lookup"><span data-stu-id="d8b08-141">Added support for change feed.</span></span>
* <span data-ttu-id="d8b08-142">Compatibilidad agregada para la recopilación de la información de cuota mediante RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="d8b08-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="d8b08-143">Compatibilidad agregada para el registro de scripts de procedimiento almacenados mediante RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="d8b08-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="d8b08-144">Se ha corregido un error en el que una consulta en modo DirectHttps puede bloquearse cuando se producen errores de limitación.</span><span class="sxs-lookup"><span data-stu-id="d8b08-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="d8b08-145">Se ha corregido un error en modo de sesión de coherencia.</span><span class="sxs-lookup"><span data-stu-id="d8b08-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="d8b08-146">Se ha corregido un error que puede causar una excepción NullReferenceException en HttpContext cuando la tasa de solicitudes es alta.</span><span class="sxs-lookup"><span data-stu-id="d8b08-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="d8b08-147">Rendimiento mejorado del modo DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="d8b08-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="d8b08-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="d8b08-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="d8b08-149">Con la API ConnectionPolicy.setProxy(), se ha agregado compatibilidad simple con proxy basada en instancias del cliente.</span><span class="sxs-lookup"><span data-stu-id="d8b08-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="d8b08-150">Se ha agregado la API DocumentClient.close() para cerrar correctamente la instancia de DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="d8b08-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="d8b08-151">Rendimiento de consultas mejorado en modo de conectividad directa al derivar el plan de consulta desde el ensamblado nativo, en lugar de hacerlo desde la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d8b08-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="d8b08-152">Se ha establecido FAIL_ON_UNKNOWN_PROPERTIES = false para que los usuarios no necesiten definir JsonIgnoreProperties en su POJO.</span><span class="sxs-lookup"><span data-stu-id="d8b08-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="d8b08-153">Se ha refactorizado el registro para que use SLF4J.</span><span class="sxs-lookup"><span data-stu-id="d8b08-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="d8b08-154">Se han corregido otros errores en el lector de coherencia.</span><span class="sxs-lookup"><span data-stu-id="d8b08-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="d8b08-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="d8b08-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="d8b08-156">Se ha corregido un error en la administración de conexiones para evitar pérdidas de conexión en el modo de conectividad directa.</span><span class="sxs-lookup"><span data-stu-id="d8b08-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="d8b08-157">Se ha corregido un error en la consulta TOP, que puede generar una excepción NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="d8b08-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="d8b08-158">Se ha mejorado el rendimiento al reducir el número de llamadas de red a las memorias caché internas.</span><span class="sxs-lookup"><span data-stu-id="d8b08-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="d8b08-159">Se ha agregado código de estado, ActivityID y la URI de la solicitud en DocumentClientException para una mejor solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="d8b08-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="d8b08-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="d8b08-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="d8b08-161">Se ha corregido un problema en la administración de las conexiones para mejorar la estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8b08-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="d8b08-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="d8b08-163">Compatibilidad agregada con el nivel de coherencia BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="d8b08-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="d8b08-164">Se ha agregado compatibilidad con la conectividad directa de las colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="d8b08-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="d8b08-165">Se ha corregido un error al realizar consultas en una base de datos con SQL.</span><span class="sxs-lookup"><span data-stu-id="d8b08-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="d8b08-166">Se ha corregido un error en la caché de sesión en la que el token de sesión puede no estar configurada correctamente.</span><span class="sxs-lookup"><span data-stu-id="d8b08-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="d8b08-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="d8b08-168">Compatibilidad agregada con las consultas paralelas entre particiones.</span><span class="sxs-lookup"><span data-stu-id="d8b08-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="d8b08-169">Se ha agregado compatibilidad con las consultas TOP y ORDER BY en las colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="d8b08-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="d8b08-170">Compatibilidad agregada con Coherencia fuerte.</span><span class="sxs-lookup"><span data-stu-id="d8b08-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="d8b08-171">Se ha agregado compatibilidad con las solicitudes basadas en nombres al utilizar la conectividad directa.</span><span class="sxs-lookup"><span data-stu-id="d8b08-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="d8b08-172">Corrección agregada para mantener la coherencia de ActivityId en todos los reintentos de solicitud.</span><span class="sxs-lookup"><span data-stu-id="d8b08-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="d8b08-173">Se ha corregido un error relacionado con la caché de sesión al volver a crear una colección con el mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="d8b08-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="d8b08-174">Se han agregado los tipos de datos Polygon y LineString al especificar la directiva de indización de colecciones para las consultas espaciales de geovallado.</span><span class="sxs-lookup"><span data-stu-id="d8b08-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="d8b08-175">Problemas corregidos con Java Doc para Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="d8b08-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="d8b08-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="d8b08-177">Se ha corregido un error en PartitionKeyDefinitionMap para almacenar en caché colecciones de partición única y no realizar solicitudes adicionales de clave de partición de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="d8b08-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="d8b08-178">Se ha corregido un error para no realizar un reintento cuando se proporcione un valor de clave de partición incorrecto.</span><span class="sxs-lookup"><span data-stu-id="d8b08-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="d8b08-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="d8b08-180">Se ha agregado compatibilidad con cuentas de base de datos de varias regiones.</span><span class="sxs-lookup"><span data-stu-id="d8b08-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="d8b08-181">Se ha agregado compatibilidad con el reintento automático en solicitudes limitadas, con opciones para personalizar el número máximo de reintentos y el tiempo de espera máximo de reintento.</span><span class="sxs-lookup"><span data-stu-id="d8b08-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="d8b08-182">Consulte RetryOptions y ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="d8b08-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="d8b08-183">Se ha dejado de utilizar el código de creación de particiones personalizado basado en IPartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="d8b08-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="d8b08-184">Utilice colecciones con particiones para conseguir un almacenamiento y un rendimiento más elevados.</span><span class="sxs-lookup"><span data-stu-id="d8b08-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="d8b08-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="d8b08-186">Se ha agregado compatibilidad con la directiva de reintentos de la limitación.</span><span class="sxs-lookup"><span data-stu-id="d8b08-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="d8b08-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="d8b08-188">Se ha agregado compatibilidad con período de vida (TTL) para los documentos.</span><span class="sxs-lookup"><span data-stu-id="d8b08-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="d8b08-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="d8b08-190">Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d8b08-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="d8b08-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="d8b08-192">Se ha corregido un error en HashPartitionResolver para generar valores hash en little endian que sean consistentes con otros SDK.</span><span class="sxs-lookup"><span data-stu-id="d8b08-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="d8b08-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="d8b08-194">Se han agregado solucionadores de particiones de hash e intervalo para ayudar con el particionamiento de las aplicaciones entre varias particiones.</span><span class="sxs-lookup"><span data-stu-id="d8b08-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="d8b08-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="d8b08-196">Implementación de Upsert.</span><span class="sxs-lookup"><span data-stu-id="d8b08-196">Implement Upsert.</span></span> <span data-ttu-id="d8b08-197">Se han agregado nuevos métodos upsertXXX para admitir la característica Upsert.</span><span class="sxs-lookup"><span data-stu-id="d8b08-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="d8b08-198">Se implementa el enrutamiento por identificador.</span><span class="sxs-lookup"><span data-stu-id="d8b08-198">Implement ID Based Routing.</span></span> <span data-ttu-id="d8b08-199">Sin cambios en la API pública, todos los cambios son internos.</span><span class="sxs-lookup"><span data-stu-id="d8b08-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="d8b08-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="d8b08-201">Versión omitida para alinear el número de versión con otros SDK</span><span class="sxs-lookup"><span data-stu-id="d8b08-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="d8b08-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="d8b08-203">Compatible con índice geoespacial.</span><span class="sxs-lookup"><span data-stu-id="d8b08-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="d8b08-204">Valida la propiedad id para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d8b08-204">Validates id property for all resources.</span></span> <span data-ttu-id="d8b08-205">Los identificadores de recursos no pueden contener los caracteres ?, /, #, \, ni terminar con un espacio.</span><span class="sxs-lookup"><span data-stu-id="d8b08-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="d8b08-206">Agrega el nuevo encabezado "progreso de transformación de índices" a ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="d8b08-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="d8b08-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="d8b08-208">Implementación de la directiva de indexación V2</span><span class="sxs-lookup"><span data-stu-id="d8b08-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="d8b08-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="d8b08-210">SDK de GA</span><span class="sxs-lookup"><span data-stu-id="d8b08-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="d8b08-211">Fechas de lanzamiento y de retirada</span><span class="sxs-lookup"><span data-stu-id="d8b08-211">Release & Retirement Dates</span></span>
<span data-ttu-id="d8b08-212">Microsoft notificará la retirada de un SDK con al menos **12 meses** de antelación para facilitar la transición a una versión compatible o más reciente.</span><span class="sxs-lookup"><span data-stu-id="d8b08-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="d8b08-213">Solo se agregan nuevas características, funcionalidad y optimizaciones al SDK actual, por lo que se recomienda actualizar siempre a la última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="d8b08-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="d8b08-214">El servicio rechazará cualquier solicitud realizada a Cosmos DB mediante un SDK retirado.</span><span class="sxs-lookup"><span data-stu-id="d8b08-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="d8b08-215">Todas las versiones del SDK de DocumentDB para Java anteriores a la versión **1.0.0** se retirarán el **29 de febrero de 2016**.</span><span class="sxs-lookup"><span data-stu-id="d8b08-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="d8b08-216">Versión</span><span class="sxs-lookup"><span data-stu-id="d8b08-216">Version</span></span> | <span data-ttu-id="d8b08-217">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="d8b08-217">Release Date</span></span> | <span data-ttu-id="d8b08-218">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="d8b08-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d8b08-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="d8b08-220">11 de julio de 2017</span><span class="sxs-lookup"><span data-stu-id="d8b08-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="d8b08-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="d8b08-222">10 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="d8b08-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="d8b08-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="d8b08-224">11 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="d8b08-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="d8b08-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="d8b08-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="d8b08-226">21 de febrero de 2017</span><span class="sxs-lookup"><span data-stu-id="d8b08-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="d8b08-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="d8b08-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="d8b08-228">31 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="d8b08-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="d8b08-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="d8b08-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="d8b08-230">24 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="d8b08-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="d8b08-232">30 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="d8b08-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="d8b08-234">28 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="d8b08-236">26 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="d8b08-238">03 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="d8b08-240">30 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="d8b08-242">14 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="d8b08-244">30 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="d8b08-246">27 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="d8b08-248">29 de marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="d8b08-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="d8b08-250">31 de diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="d8b08-252">04 de diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="d8b08-254">05 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="d8b08-256">05 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="d8b08-258">05 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="d8b08-260">09 de julio de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="d8b08-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="d8b08-262">12 de mayo de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="d8b08-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d8b08-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="d8b08-264">07 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="d8b08-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="d8b08-265">0.9.5-prelease</span></span> |<span data-ttu-id="d8b08-266">09 de marzo de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-266">Mar 09, 2015</span></span> |<span data-ttu-id="d8b08-267">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-267">February 29, 2016</span></span> |
| <span data-ttu-id="d8b08-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="d8b08-268">0.9.4-prelease</span></span> |<span data-ttu-id="d8b08-269">17 de febrero de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-269">February 17, 2015</span></span> |<span data-ttu-id="d8b08-270">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-270">February 29, 2016</span></span> |
| <span data-ttu-id="d8b08-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="d8b08-271">0.9.3-prelease</span></span> |<span data-ttu-id="d8b08-272">13 de enero de 2015</span><span class="sxs-lookup"><span data-stu-id="d8b08-272">January 13, 2015</span></span> |<span data-ttu-id="d8b08-273">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-273">February 29, 2016</span></span> |
| <span data-ttu-id="d8b08-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="d8b08-274">0.9.2-prelease</span></span> |<span data-ttu-id="d8b08-275">19 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="d8b08-275">December 19, 2014</span></span> |<span data-ttu-id="d8b08-276">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-276">February 29, 2016</span></span> |
| <span data-ttu-id="d8b08-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="d8b08-277">0.9.1-prelease</span></span> |<span data-ttu-id="d8b08-278">19 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="d8b08-278">December 19, 2014</span></span> |<span data-ttu-id="d8b08-279">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-279">February 29, 2016</span></span> |
| <span data-ttu-id="d8b08-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="d8b08-280">0.9.0-prelease</span></span> |<span data-ttu-id="d8b08-281">10 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="d8b08-281">December 10, 2014</span></span> |<span data-ttu-id="d8b08-282">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="d8b08-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="d8b08-283">P+F</span><span class="sxs-lookup"><span data-stu-id="d8b08-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="d8b08-284">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d8b08-284">See Also</span></span>
<span data-ttu-id="d8b08-285">Para más información sobre Cosmos DB, consulte la página del servicio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d8b08-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

