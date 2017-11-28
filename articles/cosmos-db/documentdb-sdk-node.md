---
title: aaaAzure Cosmos DB Node.js API, SDK y recursos | Documentos de Microsoft
description: "Infórmese acerca de hello Node.js API y SDK, incluidas las fechas de lanzamiento y fechas de retirada, los cambios realizados entre cada versión de SDK de Node.js de base de datos de Azure Cosmos Hola."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="90b17-103">SDK de Node.js para Azure Cosmos DB: notas de la versión y recursos</span><span class="sxs-lookup"><span data-stu-id="90b17-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90b17-104">.NET</span><span class="sxs-lookup"><span data-stu-id="90b17-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="90b17-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="90b17-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="90b17-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="90b17-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="90b17-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="90b17-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="90b17-108">Java</span><span class="sxs-lookup"><span data-stu-id="90b17-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="90b17-109">Python</span><span class="sxs-lookup"><span data-stu-id="90b17-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="90b17-110">REST</span><span class="sxs-lookup"><span data-stu-id="90b17-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="90b17-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="90b17-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="90b17-112">SQL</span><span class="sxs-lookup"><span data-stu-id="90b17-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="90b17-113">**Descargar SDK**</span><span class="sxs-lookup"><span data-stu-id="90b17-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="90b17-114">NPM</span><span class="sxs-lookup"><span data-stu-id="90b17-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="90b17-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="90b17-115">**API documentation**</span></span></td><td>[<span data-ttu-id="90b17-116">Documentación de referencia de la API de Node.js</span><span class="sxs-lookup"><span data-stu-id="90b17-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="90b17-117">**Instrucciones de instalación del SDK**</span><span class="sxs-lookup"><span data-stu-id="90b17-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="90b17-118">Instrucciones de instalación</span><span class="sxs-lookup"><span data-stu-id="90b17-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="90b17-119">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="90b17-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="90b17-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="90b17-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="90b17-121">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="90b17-121">**Samples**</span></span></td><td>[<span data-ttu-id="90b17-122">Ejemplos de código Node.js</span><span class="sxs-lookup"><span data-stu-id="90b17-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="90b17-123">**Tutorial introductorio**</span><span class="sxs-lookup"><span data-stu-id="90b17-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="90b17-124">Empezar a trabajar con hello SDK de Node.js</span><span class="sxs-lookup"><span data-stu-id="90b17-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="90b17-125">**Tutorial de la aplicación web**</span><span class="sxs-lookup"><span data-stu-id="90b17-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="90b17-126">Creación de una aplicación web de Node.js con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90b17-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="90b17-127">**Plataforma admitida actualmente**</span><span class="sxs-lookup"><span data-stu-id="90b17-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="90b17-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="90b17-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="90b17-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="90b17-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="90b17-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="90b17-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="90b17-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="90b17-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="90b17-132">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="90b17-132">Release notes</span></span>

### <span data-ttu-id="90b17-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="90b17-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="90b17-134">Documentación de NPM corregida.</span><span class="sxs-lookup"><span data-stu-id="90b17-134">npm documentation fixed.</span></span>

### <span data-ttu-id="90b17-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="90b17-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="90b17-136">Se ha corregido un error en executeStoredProcedure en el que los documentos implicados tenían caracteres especiales de Unicode (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="90b17-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="90b17-137">Se ha corregido un error en el control de documentos con caracteres Unicode en la clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="90b17-138">Compatibilidad fijo para crear colecciones con medios de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="90b17-139">Problema de GitHub n.º 114.</span><span class="sxs-lookup"><span data-stu-id="90b17-139">Github issue #114.</span></span>
* <span data-ttu-id="90b17-140">Se ha corregido el problema de compatibilidad con el token de autorización de permiso.</span><span class="sxs-lookup"><span data-stu-id="90b17-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="90b17-141">Problema de GitHub n.º 178.</span><span class="sxs-lookup"><span data-stu-id="90b17-141">Github issue #178.</span></span>

### <span data-ttu-id="90b17-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="90b17-143">Se agregó compatibilidad con un nuevo [nivel de coherencia](consistency-levels.md) denominado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="90b17-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="90b17-144">Se agregó compatibilidad con UriFactory.</span><span class="sxs-lookup"><span data-stu-id="90b17-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="90b17-145">Se ha corregido un error de compatibilidad con Unicode.</span><span class="sxs-lookup"><span data-stu-id="90b17-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="90b17-146">Problema de GitHub n.º 171.</span><span class="sxs-lookup"><span data-stu-id="90b17-146">GitHub issue #171.</span></span>

### <span data-ttu-id="90b17-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="90b17-148">Compatibilidad de hello agregados para consultas de agregación (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="90b17-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="90b17-149">Opción de hello agregada para controlar el grado de paralelismo para entre las consultas de partición.</span><span class="sxs-lookup"><span data-stu-id="90b17-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="90b17-150">Opción de hello agregada para deshabilitar la comprobación de SSL cuando se ejecuta en el emulador de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="90b17-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="90b17-151">Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="90b17-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="90b17-152">Error de token de continuación de hello fijo para la recopilación de una única partición.</span><span class="sxs-lookup"><span data-stu-id="90b17-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="90b17-153">Problema de GitHub n.º 107.</span><span class="sxs-lookup"><span data-stu-id="90b17-153">Github issue #107.</span></span>
* <span data-ttu-id="90b17-154">Error de executeStoredProcedure Hola fijo en el control de 0 como parámetro único.</span><span class="sxs-lookup"><span data-stu-id="90b17-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="90b17-155">Problema de GitHub n.º 155.</span><span class="sxs-lookup"><span data-stu-id="90b17-155">Github issue #155.</span></span>

### <span data-ttu-id="90b17-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="90b17-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="90b17-157">Versión del agente de usuario fijo encabezado tooinclude Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="90b17-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="90b17-158">Limpieza menor de código.</span><span class="sxs-lookup"><span data-stu-id="90b17-158">Minor code cleanup.</span></span>

### <span data-ttu-id="90b17-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="90b17-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="90b17-160">Deshabilitar la comprobación de SSL al usar Hola SDK tootarget hello emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="90b17-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="90b17-161">Se ha agregado compatibilidad para habilitar el registro de scripts durante la ejecución de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="90b17-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="90b17-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="90b17-163">Compatibilidad agregada con las consultas paralelas entre particiones.</span><span class="sxs-lookup"><span data-stu-id="90b17-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="90b17-164">Se ha agregado compatibilidad con las consultas TOP y ORDER BY en las colecciones particionadas.</span><span class="sxs-lookup"><span data-stu-id="90b17-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="90b17-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="90b17-166">Se ha agregado compatibilidad de la directiva de reintentos con las solicitudes de limitación.</span><span class="sxs-lookup"><span data-stu-id="90b17-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="90b17-167">(Las solicitudes limitadas reciben una excepción demasiado grande de la tasa de solicitudes, código de error 429). De forma predeterminada, base de datos de Azure Cosmos reintenta nueve veces para cada solicitud cuando se encuentra el código de error 429, teniendo en cuenta el tiempo de retryAfter de hello en el encabezado de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="90b17-168">Un tiempo de intervalo de reintento fijo ahora pueden establecer como parte del programa Hola propiedad RetryOptions en hello ConnectionPolicy objeto si desea tooignore hello retryAfter tiempo devuelto por servidor entre los reintentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="90b17-169">Base de datos de Azure Cosmos ahora espera durante un máximo de 30 segundos para cada solicitud que se está limitando (independientemente del número de reintentos) y devuelve la respuesta de hello con código de error 429.</span><span class="sxs-lookup"><span data-stu-id="90b17-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="90b17-170">Esta vez también puede invalidarse en hello RetryOptions propiedad ConnectionPolicy objeto.</span><span class="sxs-lookup"><span data-stu-id="90b17-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="90b17-171">COSMOS DB ahora devuelve x-ms-acelerador--número de reintentos y x-ms-throttle-retry-wait-time-ms como encabezados de respuesta de hello en cada Acelerador de saludo de solicitud toodenote tiempo de reintento hello y recuento acumulado Hola solicitar esperado entre reintentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="90b17-172">Hola RetryOptions clase se ha agregado, exposición hello RetryOptions propiedad en una clase ConnectionPolicy Hola que puede ser utilizado toooverride algunos predeterminado Hola opciones de reintento.</span><span class="sxs-lookup"><span data-stu-id="90b17-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="90b17-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="90b17-174">Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.</span><span class="sxs-lookup"><span data-stu-id="90b17-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="90b17-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="90b17-176">Hola agregado compatibilidad con característica de tooLive(TTL) de tiempo para los documentos.</span><span class="sxs-lookup"><span data-stu-id="90b17-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="90b17-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="90b17-178">Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="90b17-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="90b17-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="90b17-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="90b17-180">Corregido el error RangePartitionResolver.resolveForRead donde no devolvían vínculos debido tooa concat incorrecta de resultados.</span><span class="sxs-lookup"><span data-stu-id="90b17-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="90b17-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="90b17-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="90b17-182">Valor hashParitionResolver resolveForRead() fijo: cuando ninguna clave de partición proporcionada lanzó una excepción, en lugar de devolver una lista de todos los vínculos registrados.</span><span class="sxs-lookup"><span data-stu-id="90b17-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="90b17-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="90b17-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="90b17-184">Corrige el problema [&#100;](https://github.com/Azure/azure-documentdb-node/issues/100) -agente de HTTPS dedicado: evitar modificar global de los agentes Hola para fines de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="90b17-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="90b17-185">Usar a un agente dedicado para todas las solicitudes de lib Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="90b17-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="90b17-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="90b17-187">Corrige el problema [81](https://github.com/Azure/azure-documentdb-node/issues/81) : controla correctamente guiones en identificadores de medios.</span><span class="sxs-lookup"><span data-stu-id="90b17-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="90b17-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="90b17-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="90b17-189">Corrige el problema [95](https://github.com/Azure/azure-documentdb-node/issues/95) : advertencia de pérdida de escucha de EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="90b17-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="90b17-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="90b17-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="90b17-191">Corrige el problema [&#92;](https://github.com/Azure/azure-documentdb-node/issues/90) -cambiar el nombre de carpeta toohash de Hash para los sistemas entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="90b17-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="90b17-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="90b17-193">Se implementa la compatibilidad con el particionamiento, para lo que se agregan resolvedores de hash y de particiones de intervalo.</span><span class="sxs-lookup"><span data-stu-id="90b17-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="90b17-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="90b17-195">Implementación de Upsert.</span><span class="sxs-lookup"><span data-stu-id="90b17-195">Implement Upsert.</span></span> <span data-ttu-id="90b17-196">Se han agregado nuevos métodos upsertXXX en documentClient.</span><span class="sxs-lookup"><span data-stu-id="90b17-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="90b17-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="90b17-198">Omite los números de versión de toobring en consonancia con el resto de SDK.</span><span class="sxs-lookup"><span data-stu-id="90b17-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="90b17-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="90b17-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="90b17-200">Preguntas de división promete repositorio toonew de contenedor.</span><span class="sxs-lookup"><span data-stu-id="90b17-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="90b17-201">Actualizar toopackage archivo de registro de npm.</span><span class="sxs-lookup"><span data-stu-id="90b17-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="90b17-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="90b17-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="90b17-203">Se implementa el enrutamiento por identificador.</span><span class="sxs-lookup"><span data-stu-id="90b17-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="90b17-204">Corrige el problema [49](https://github.com/Azure/azure-documentdb-node/issues/49) : la propiedad current entra en conflicto con el método current().</span><span class="sxs-lookup"><span data-stu-id="90b17-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="90b17-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="90b17-206">Se agregó compatibilidad con índice geoespacial.</span><span class="sxs-lookup"><span data-stu-id="90b17-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="90b17-207">Valida la propiedad id para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="90b17-207">Validates id property for all resources.</span></span> <span data-ttu-id="90b17-208">Los identificadores de recursos no pueden contener los caracteres ?, /, #, &#47;&#47;, ni terminar con un espacio.</span><span class="sxs-lookup"><span data-stu-id="90b17-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="90b17-209">Agrega el nuevo encabezado "curso de transformación de índice" tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="90b17-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="90b17-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="90b17-211">Implementación de la directiva de indexación V2.</span><span class="sxs-lookup"><span data-stu-id="90b17-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="90b17-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="90b17-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="90b17-213">Problema [&#40;](https://github.com/Azure/azure-documentdb-node/issues/40) : implementa eslint y grunt configuraciones en el núcleo de Hola y promesa SDK.</span><span class="sxs-lookup"><span data-stu-id="90b17-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="90b17-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="90b17-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="90b17-215">Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) : el contenedor de objetos promise no incluye el encabezado con el error.</span><span class="sxs-lookup"><span data-stu-id="90b17-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="90b17-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="90b17-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="90b17-217">Implementa tooquery capacidad si hay conflictos agregando readConflicts, readConflictAsync y queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="90b17-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="90b17-218">Documentación de la API actualizada.</span><span class="sxs-lookup"><span data-stu-id="90b17-218">Updated API documentation.</span></span>
* <span data-ttu-id="90b17-219">Problema [41](https://github.com/Azure/azure-documentdb-node/issues/41) : error client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="90b17-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="90b17-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="90b17-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="90b17-221">SDK de GA.</span><span class="sxs-lookup"><span data-stu-id="90b17-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="90b17-222">Fechas de lanzamiento y de retirada</span><span class="sxs-lookup"><span data-stu-id="90b17-222">Release & Retirement Dates</span></span>
<span data-ttu-id="90b17-223">Microsoft proporciona una notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.</span><span class="sxs-lookup"><span data-stu-id="90b17-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="90b17-224">Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, como por ejemplo, se recomienda que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="90b17-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="90b17-225">Cualquier solicitud tooCosmos base de datos con un SDK retirado es ser rechazados por el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b17-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="90b17-226">Versión</span><span class="sxs-lookup"><span data-stu-id="90b17-226">Version</span></span> | <span data-ttu-id="90b17-227">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="90b17-227">Release Date</span></span> | <span data-ttu-id="90b17-228">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="90b17-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="90b17-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="90b17-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="90b17-230">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="90b17-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="90b17-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="90b17-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="90b17-232">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="90b17-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="90b17-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="90b17-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="90b17-234">10 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="90b17-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="90b17-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="90b17-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="90b17-236">16 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="90b17-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="90b17-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="90b17-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="90b17-238">27 de enero de 2017</span><span class="sxs-lookup"><span data-stu-id="90b17-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="90b17-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="90b17-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="90b17-240">22 de diciembre de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="90b17-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="90b17-242">03 de octubre de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="90b17-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="90b17-244">7 de julio de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="90b17-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="90b17-246">14 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="90b17-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="90b17-248">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="90b17-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="90b17-250">29 de marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="90b17-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="90b17-252">8 de marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="90b17-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="90b17-254">2 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="90b17-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="90b17-256">1 de febrero de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="90b17-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="90b17-258">26 de enero de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="90b17-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="90b17-260">22 de enero de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="90b17-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="90b17-262">4 de enero de 2016</span><span class="sxs-lookup"><span data-stu-id="90b17-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="90b17-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="90b17-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="90b17-264">31 de diciembre de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="90b17-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="90b17-266">6 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="90b17-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="90b17-268">6 de octubre de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="90b17-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="90b17-270">10 de septiembre de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="90b17-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="90b17-272">15 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="90b17-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="90b17-274">05 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="90b17-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="90b17-276">09 de julio de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="90b17-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="90b17-278">4 de junio de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="90b17-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="90b17-280">23 de mayo de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="90b17-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="90b17-282">15 de mayo de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="90b17-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="90b17-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="90b17-284">08 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="90b17-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="90b17-285">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="90b17-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="90b17-286">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="90b17-286">See also</span></span>
<span data-ttu-id="90b17-287">toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.</span><span class="sxs-lookup"><span data-stu-id="90b17-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

