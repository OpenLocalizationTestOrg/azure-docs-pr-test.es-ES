---
title: API, SDK y recursos de Python para Azure Cosmos DB | Microsoft Docs
description: "Obtenga toda la información sobre la API y el SDK de Python incluidas la fechas de lanzamiento, fechas de retirada y cambios realizados entre las versiones del SDK de Python para Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="ace05-103">SDK de Python para Azure Cosmos DB: notas de la versión y recursos</span><span class="sxs-lookup"><span data-stu-id="ace05-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ace05-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ace05-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="ace05-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="ace05-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="ace05-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ace05-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="ace05-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="ace05-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="ace05-108">Java</span><span class="sxs-lookup"><span data-stu-id="ace05-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="ace05-109">Python</span><span class="sxs-lookup"><span data-stu-id="ace05-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="ace05-110">REST</span><span class="sxs-lookup"><span data-stu-id="ace05-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="ace05-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="ace05-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="ace05-112">SQL</span><span class="sxs-lookup"><span data-stu-id="ace05-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="ace05-113">**Descargar SDK**</span><span class="sxs-lookup"><span data-stu-id="ace05-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="ace05-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="ace05-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="ace05-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="ace05-115">**API documentation**</span></span></td><td>[<span data-ttu-id="ace05-116">Documentación de referencia de la API de Python</span><span class="sxs-lookup"><span data-stu-id="ace05-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="ace05-117">**Instrucciones de instalación del SDK**</span><span class="sxs-lookup"><span data-stu-id="ace05-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="ace05-118">Instrucciones de instalación del SDK de Python</span><span class="sxs-lookup"><span data-stu-id="ace05-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="ace05-119">**Contribuya al SDK**</span><span class="sxs-lookup"><span data-stu-id="ace05-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="ace05-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="ace05-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="ace05-121">**Primeros pasos**</span><span class="sxs-lookup"><span data-stu-id="ace05-121">**Get started**</span></span></td><td>[<span data-ttu-id="ace05-122">Introducción al SDK de Python</span><span class="sxs-lookup"><span data-stu-id="ace05-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="ace05-123">**Plataforma admitida actualmente**</span><span class="sxs-lookup"><span data-stu-id="ace05-123">**Current supported platform**</span></span></td><td><span data-ttu-id="ace05-124">[Python 2.7](https://www.python.org/downloads/) y [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ace05-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="ace05-125">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="ace05-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="ace05-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="ace05-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="ace05-127">Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="ace05-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="ace05-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="ace05-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="ace05-129">Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="ace05-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="ace05-130">Se agregó una opción para deshabilitar la comprobación de SSL cuando se ejecuta en el emulador de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ace05-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="ace05-131">Se ha quitado la restricción del módulo de solicitudes dependientes para que sea exactamente 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="ace05-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="ace05-132">Reducción del procesamiento mínimo en las colecciones particionadas de 10 100 RU/s a 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="ace05-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="ace05-133">Se ha agregado compatibilidad para habilitar el registro de scripts durante la ejecución de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="ace05-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="ace05-134">La versión de API de REST se incrementó a "2017-01-19" con esta versión.</span><span class="sxs-lookup"><span data-stu-id="ace05-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="ace05-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="ace05-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="ace05-136">Se realizan los cambios editoriales de los comentarios de documentación.</span><span class="sxs-lookup"><span data-stu-id="ace05-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="ace05-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="ace05-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="ace05-138">Compatibilidad agregada para Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="ace05-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="ace05-139">Compatibilidad agregada para agrupaciones de conexiones con un módulo de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="ace05-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="ace05-140">Compatibilidad agregada para la coherencia de la sesión.</span><span class="sxs-lookup"><span data-stu-id="ace05-140">Added support for session consistency.</span></span>
* <span data-ttu-id="ace05-141">Compatibilidad agregada para consultas TOP/ORDERBY para colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="ace05-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="ace05-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="ace05-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="ace05-143">Se ha agregado compatibilidad de la directiva de reintentos con las solicitudes de limitación.</span><span class="sxs-lookup"><span data-stu-id="ace05-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="ace05-144">(Las solicitudes limitadas reciben una excepción demasiado grande de la tasa de solicitudes, código de error 429). De manera predeterminada, Azure Cosmos DB realiza nueve reintentos para cada solicitud cuando aparece el código de error 429, respetando el tiempo de retryAfter en el encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ace05-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="ace05-145">Ahora puede establecerse un tiempo del intervalo de reintento fijo como parte de la propiedad RetryOptions del objeto ConnectionPolicy si quiere ignorar el tiempo de retryAfter que ha devuelto el servidor entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="ace05-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="ace05-146">Azure Cosmos DB espera ahora un máximo de 30 segundos para cada solicitud que se está limitando (independientemente del recuento de reintentos) y devuelve la respuesta con el código de error 429.</span><span class="sxs-lookup"><span data-stu-id="ace05-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="ace05-147">Este tiempo también puede reemplazarse en la propiedad RetryOptions del objeto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="ace05-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="ace05-148">Cosmos DB ahora devuelve x-ms-throttle-retry-count y x-ms-throttle-retry-wait-time-ms como los encabezados de respuesta de cada solicitud para denotar el recuento de reintentos de limitación y el tiempo acumulativo que ha esperado la solicitud entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="ace05-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="ace05-149">Se ha quitado la clase RetryPolicy y la propiedad correspondiente (retry_policy) que estaba expuesta en la clase document_client y, en su lugar, se ha introducido una clase RetryOptions que expone la propiedad RetryOptions en la clase ConnectionPolicy que puede usarse para reemplazar algunas de las opciones de reintentos predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="ace05-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="ace05-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="ace05-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="ace05-151">Se ha agregado compatibilidad con cuentas de base de datos de varias regiones.</span><span class="sxs-lookup"><span data-stu-id="ace05-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="ace05-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="ace05-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="ace05-153">Se ha agregado compatibilidad con la característica de período de vida (TTL) para los documentos.</span><span class="sxs-lookup"><span data-stu-id="ace05-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="ace05-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="ace05-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="ace05-155">Correcciones de errores relacionados con la creación de particiones del lado servidor para permitir caracteres especiales en la ruta de acceso de la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="ace05-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="ace05-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="ace05-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="ace05-157">Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ace05-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="ace05-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="ace05-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="ace05-159">Se han agregado solucionadores de particiones de hash e intervalo para ayudar con el particionamiento de las aplicaciones entre varias particiones.</span><span class="sxs-lookup"><span data-stu-id="ace05-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="ace05-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="ace05-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="ace05-161">Implementación de Upsert.</span><span class="sxs-lookup"><span data-stu-id="ace05-161">Implement Upsert.</span></span> <span data-ttu-id="ace05-162">Se han agregado nuevos métodos upsertXXX para admitir la característica Upsert.</span><span class="sxs-lookup"><span data-stu-id="ace05-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="ace05-163">Se implementa el enrutamiento por identificador.</span><span class="sxs-lookup"><span data-stu-id="ace05-163">Implement ID Based Routing.</span></span> <span data-ttu-id="ace05-164">Sin cambios en la API pública, todos los cambios son internos.</span><span class="sxs-lookup"><span data-stu-id="ace05-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="ace05-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="ace05-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="ace05-166">Compatible con índice geoespacial.</span><span class="sxs-lookup"><span data-stu-id="ace05-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="ace05-167">Valida la propiedad id para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ace05-167">Validates id property for all resources.</span></span> <span data-ttu-id="ace05-168">Los identificadores de recursos no pueden contener los caracteres ?, /, #, \, ni terminar con un espacio.</span><span class="sxs-lookup"><span data-stu-id="ace05-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="ace05-169">Agrega el nuevo encabezado "progreso de transformación de índices" a ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="ace05-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="ace05-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="ace05-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="ace05-171">Implementación de la directiva de indexación V2.</span><span class="sxs-lookup"><span data-stu-id="ace05-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="ace05-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="ace05-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="ace05-173">Compatibilidad con conexión de proxy.</span><span class="sxs-lookup"><span data-stu-id="ace05-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="ace05-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="ace05-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="ace05-175">SDK de GA.</span><span class="sxs-lookup"><span data-stu-id="ace05-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="ace05-176">Fechas de lanzamiento y retirada</span><span class="sxs-lookup"><span data-stu-id="ace05-176">Release & retirement dates</span></span>
<span data-ttu-id="ace05-177">Microsoft notificará la retirada de un SDK con al menos **12 meses** de antelación para facilitar la transición a una versión compatible o más reciente.</span><span class="sxs-lookup"><span data-stu-id="ace05-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="ace05-178">Solo se agregan nuevas características, funcionalidad y optimizaciones al SDK actual, por lo que se recomienda actualizar siempre a la última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="ace05-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="ace05-179">El servicio rechazará cualquier solicitud realizada a Cosmos DB mediante un SDK retirado.</span><span class="sxs-lookup"><span data-stu-id="ace05-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="ace05-180">Todas las versiones del SDK de Azure DocumentDB para Python anteriores a la versión **1.0.0** se retirarán el **29 de febrero de 2016**.</span><span class="sxs-lookup"><span data-stu-id="ace05-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="ace05-181">Versión</span><span class="sxs-lookup"><span data-stu-id="ace05-181">Version</span></span> | <span data-ttu-id="ace05-182">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="ace05-182">Release Date</span></span> | <span data-ttu-id="ace05-183">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="ace05-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="ace05-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="ace05-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="ace05-185">10 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="ace05-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="ace05-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="ace05-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="ace05-187">1 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="ace05-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="ace05-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="ace05-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="ace05-189">30 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ace05-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="ace05-191">29 de septiembre de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="ace05-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="ace05-193">7 de julio de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="ace05-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="ace05-195">14 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="ace05-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="ace05-197">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="ace05-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="ace05-199">08 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="ace05-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="ace05-201">29 de marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="ace05-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="ace05-203">3 de enero de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="ace05-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="ace05-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="ace05-205">6 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="ace05-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="ace05-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="ace05-207">6 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="ace05-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="ace05-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="ace05-209">6 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="ace05-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="ace05-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="ace05-211">09 de julio de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="ace05-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="ace05-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="ace05-213">25 de mayo de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="ace05-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ace05-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="ace05-215">07 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="ace05-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="ace05-216">0.9.4-prelease</span></span> |<span data-ttu-id="ace05-217">14 de enero de 2015</span><span class="sxs-lookup"><span data-stu-id="ace05-217">January 14, 2015</span></span> |<span data-ttu-id="ace05-218">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-218">February 29, 2016</span></span> |
| <span data-ttu-id="ace05-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="ace05-219">0.9.3-prelease</span></span> |<span data-ttu-id="ace05-220">9 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="ace05-220">December 09, 2014</span></span> |<span data-ttu-id="ace05-221">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-221">February 29, 2016</span></span> |
| <span data-ttu-id="ace05-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="ace05-222">0.9.2-prelease</span></span> |<span data-ttu-id="ace05-223">25 de noviembre de 2014</span><span class="sxs-lookup"><span data-stu-id="ace05-223">November 25, 2014</span></span> |<span data-ttu-id="ace05-224">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-224">February 29, 2016</span></span> |
| <span data-ttu-id="ace05-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="ace05-225">0.9.1-prelease</span></span> |<span data-ttu-id="ace05-226">23 de septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="ace05-226">September 23, 2014</span></span> |<span data-ttu-id="ace05-227">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-227">February 29, 2016</span></span> |
| <span data-ttu-id="ace05-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="ace05-228">0.9.0-prelease</span></span> |<span data-ttu-id="ace05-229">21 de agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="ace05-229">August 21, 2014</span></span> |<span data-ttu-id="ace05-230">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="ace05-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="ace05-231">P+F</span><span class="sxs-lookup"><span data-stu-id="ace05-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="ace05-232">Consulte también</span><span class="sxs-lookup"><span data-stu-id="ace05-232">See also</span></span>
<span data-ttu-id="ace05-233">Para más información sobre Cosmos DB, consulte la página del servicio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ace05-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

