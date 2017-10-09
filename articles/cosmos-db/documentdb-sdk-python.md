---
title: aaaAzure Cosmos DB Python API, SDK y recursos | Documentos de Microsoft
description: "Infórmese acerca de hello Python API y SDK, incluidas las fechas de lanzamiento y fechas de retirada, los cambios realizados entre cada versión de hello Azure Cosmos DB Python SDK."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="6c8cd-103">SDK de Python para Azure Cosmos DB: notas de la versión y recursos</span><span class="sxs-lookup"><span data-stu-id="6c8cd-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c8cd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6c8cd-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="6c8cd-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="6c8cd-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="6c8cd-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6c8cd-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="6c8cd-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="6c8cd-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="6c8cd-108">Java</span><span class="sxs-lookup"><span data-stu-id="6c8cd-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="6c8cd-109">Python</span><span class="sxs-lookup"><span data-stu-id="6c8cd-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="6c8cd-110">REST</span><span class="sxs-lookup"><span data-stu-id="6c8cd-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="6c8cd-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="6c8cd-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="6c8cd-112">SQL</span><span class="sxs-lookup"><span data-stu-id="6c8cd-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="6c8cd-113">**Descargar SDK**</span><span class="sxs-lookup"><span data-stu-id="6c8cd-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="6c8cd-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="6c8cd-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="6c8cd-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="6c8cd-115">**API documentation**</span></span></td><td>[<span data-ttu-id="6c8cd-116">Documentación de referencia de la API de Python</span><span class="sxs-lookup"><span data-stu-id="6c8cd-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="6c8cd-117">**Instrucciones de instalación del SDK**</span><span class="sxs-lookup"><span data-stu-id="6c8cd-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="6c8cd-118">Instrucciones de instalación del SDK de Python</span><span class="sxs-lookup"><span data-stu-id="6c8cd-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="6c8cd-119">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="6c8cd-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="6c8cd-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="6c8cd-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="6c8cd-121">**Introducción**</span><span class="sxs-lookup"><span data-stu-id="6c8cd-121">**Get started**</span></span></td><td>[<span data-ttu-id="6c8cd-122">Empezar a trabajar con hello SDK de Python</span><span class="sxs-lookup"><span data-stu-id="6c8cd-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="6c8cd-123">**Plataforma admitida actualmente**</span><span class="sxs-lookup"><span data-stu-id="6c8cd-123">**Current supported platform**</span></span></td><td><span data-ttu-id="6c8cd-124">[Python 2.7](https://www.python.org/downloads/) y [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="6c8cd-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="6c8cd-125">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="6c8cd-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="6c8cd-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="6c8cd-127">Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="6c8cd-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="6c8cd-129">Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="6c8cd-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="6c8cd-130">Se agregó una opción para deshabilitar la comprobación de SSL cuando se ejecuta en el emulador de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="6c8cd-131">Quitar restricción de Hola de las solicitudes dependientes módulo toobe 2.10.0 exactamente.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="6c8cd-132">Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="6c8cd-133">Se ha agregado compatibilidad para habilitar el registro de scripts durante la ejecución de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="6c8cd-134">Versión de API de REST demasiado incrementará ' 2017-01-19' con esta versión.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="6c8cd-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="6c8cd-136">Realiza los cambios editoriales toodocumentation comentarios.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="6c8cd-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="6c8cd-138">Compatibilidad agregada para Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="6c8cd-139">Compatibilidad agregada para agrupaciones de conexiones con un módulo de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="6c8cd-140">Compatibilidad agregada para la coherencia de la sesión.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-140">Added support for session consistency.</span></span>
* <span data-ttu-id="6c8cd-141">Compatibilidad agregada para consultas TOP/ORDERBY para colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="6c8cd-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="6c8cd-143">Se ha agregado compatibilidad de la directiva de reintentos con las solicitudes de limitación.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="6c8cd-144">(Las solicitudes limitadas reciben una excepción demasiado grande de la tasa de solicitudes, código de error 429). De forma predeterminada, base de datos de Azure Cosmos reintenta nueve veces para cada solicitud cuando se encuentra el código de error 429, teniendo en cuenta el tiempo de retryAfter de hello en el encabezado de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="6c8cd-145">Un tiempo de intervalo de reintento fijo ahora pueden establecer como parte del programa Hola propiedad RetryOptions en hello ConnectionPolicy objeto si desea tooignore hello retryAfter tiempo devuelto por servidor entre los reintentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="6c8cd-146">Base de datos de Azure Cosmos ahora espera durante un máximo de 30 segundos para cada solicitud que se está limitando (independientemente del número de reintentos) y devuelve la respuesta de hello con código de error 429.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="6c8cd-147">Esta vez también puede ser reemplazada en hello RetryOptions propiedad ConnectionPolicy objeto.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="6c8cd-148">COSMOS DB ahora devuelve x-ms-acelerador--número de reintentos y x-ms-throttle-retry-wait-time-ms como encabezados de respuesta de hello en cada Acelerador de saludo de solicitud toodenote tiempo de reintento hello y recuento cummulative Hola solicitar esperado entre reintentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="6c8cd-149">Clase de RetryPolicy de hello quitado y la propiedad correspondiente de hello (retry_policy) exponen en clase document_client de hello e introdujeron en su lugar una clase RetryOptions exposición hello RetryOptions propiedad en una clase ConnectionPolicy que puede ser utilizado toooverride Algunos predeterminado Hola opciones de reintento.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="6c8cd-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="6c8cd-151">Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="6c8cd-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="6c8cd-153">Hola agregado compatibilidad con característica de tooLive(TTL) de tiempo para los documentos.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="6c8cd-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="6c8cd-155">Correcciones de errores relacionados con lado tooserver particiones tooallow caracteres especiales en la ruta de acceso de partitionkey.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="6c8cd-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="6c8cd-157">Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6c8cd-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="6c8cd-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="6c8cd-159">Agregar Hash & intervalo tooassist de resoluciones de partición con aplicaciones de particionamiento entre varias particiones.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="6c8cd-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="6c8cd-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="6c8cd-161">Implementación de Upsert.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-161">Implement Upsert.</span></span> <span data-ttu-id="6c8cd-162">Nuevos métodos de UpsertXXX agregan toosupport Upsert característica.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="6c8cd-163">Se implementa el enrutamiento por identificador.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-163">Implement ID Based Routing.</span></span> <span data-ttu-id="6c8cd-164">Sin cambios en la API pública, todos los cambios son internos.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="6c8cd-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="6c8cd-166">Compatible con índice geoespacial.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="6c8cd-167">Valida la propiedad id para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-167">Validates id property for all resources.</span></span> <span data-ttu-id="6c8cd-168">Los identificadores de recursos no pueden contener los caracteres ?, /, #, \, ni terminar con un espacio.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="6c8cd-169">Agrega el nuevo encabezado "curso de transformación de índice" tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="6c8cd-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="6c8cd-171">Implementación de la directiva de indexación V2.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="6c8cd-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="6c8cd-173">Compatibilidad con conexión de proxy.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="6c8cd-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="6c8cd-175">SDK de GA.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="6c8cd-176">Fechas de lanzamiento y retirada</span><span class="sxs-lookup"><span data-stu-id="6c8cd-176">Release & retirement dates</span></span>
<span data-ttu-id="6c8cd-177">Microsoft proporcionará la notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="6c8cd-178">Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, por lo tanto, es recomendable que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="6c8cd-179">Servicio de hello rechazará cualquier base de datos con un SDK retirado tooCosmos de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="6c8cd-180">Todas las versiones de hello documentos de Azure SDK para Python anterior tooversion **1.0.0** se retirarán en **29 de febrero de 2016**.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="6c8cd-181">Versión</span><span class="sxs-lookup"><span data-stu-id="6c8cd-181">Version</span></span> | <span data-ttu-id="6c8cd-182">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="6c8cd-182">Release Date</span></span> | <span data-ttu-id="6c8cd-183">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="6c8cd-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="6c8cd-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="6c8cd-185">10 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="6c8cd-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="6c8cd-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="6c8cd-187">1 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="6c8cd-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="6c8cd-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="6c8cd-189">30 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="6c8cd-191">29 de septiembre de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="6c8cd-193">7 de julio de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="6c8cd-195">14 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="6c8cd-197">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="6c8cd-199">08 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="6c8cd-201">29 de marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="6c8cd-203">3 de enero de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="6c8cd-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="6c8cd-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="6c8cd-205">6 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="6c8cd-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="6c8cd-207">6 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="6c8cd-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="6c8cd-209">6 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="6c8cd-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="6c8cd-211">09 de julio de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="6c8cd-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="6c8cd-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="6c8cd-213">25 de mayo de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="6c8cd-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8cd-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="6c8cd-215">07 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="6c8cd-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="6c8cd-216">0.9.4-prelease</span></span> |<span data-ttu-id="6c8cd-217">14 de enero de 2015</span><span class="sxs-lookup"><span data-stu-id="6c8cd-217">January 14, 2015</span></span> |<span data-ttu-id="6c8cd-218">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-218">February 29, 2016</span></span> |
| <span data-ttu-id="6c8cd-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="6c8cd-219">0.9.3-prelease</span></span> |<span data-ttu-id="6c8cd-220">9 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="6c8cd-220">December 09, 2014</span></span> |<span data-ttu-id="6c8cd-221">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-221">February 29, 2016</span></span> |
| <span data-ttu-id="6c8cd-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="6c8cd-222">0.9.2-prelease</span></span> |<span data-ttu-id="6c8cd-223">25 de noviembre de 2014</span><span class="sxs-lookup"><span data-stu-id="6c8cd-223">November 25, 2014</span></span> |<span data-ttu-id="6c8cd-224">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-224">February 29, 2016</span></span> |
| <span data-ttu-id="6c8cd-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="6c8cd-225">0.9.1-prelease</span></span> |<span data-ttu-id="6c8cd-226">23 de septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="6c8cd-226">September 23, 2014</span></span> |<span data-ttu-id="6c8cd-227">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-227">February 29, 2016</span></span> |
| <span data-ttu-id="6c8cd-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="6c8cd-228">0.9.0-prelease</span></span> |<span data-ttu-id="6c8cd-229">21 de agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="6c8cd-229">August 21, 2014</span></span> |<span data-ttu-id="6c8cd-230">29 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="6c8cd-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="6c8cd-231">P+F</span><span class="sxs-lookup"><span data-stu-id="6c8cd-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="6c8cd-232">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6c8cd-232">See also</span></span>
<span data-ttu-id="6c8cd-233">toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.</span><span class="sxs-lookup"><span data-stu-id="6c8cd-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

