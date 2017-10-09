---
title: aaaAzure Cosmos DB .NET Core API, SDK y recursos | Documentos de Microsoft
description: "Infórmese acerca de hello .NET Core API y SDK, incluidas las fechas de lanzamiento y fechas de retirada, los cambios realizados entre cada versión de hello Azure Cosmos DB .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="7c827-103">SDK de .NET Core para Azure Cosmos DB: notas de la versión y recursos</span><span class="sxs-lookup"><span data-stu-id="7c827-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c827-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7c827-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="7c827-105">Fuente de cambios de .NET</span><span class="sxs-lookup"><span data-stu-id="7c827-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="7c827-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7c827-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="7c827-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="7c827-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="7c827-108">Java</span><span class="sxs-lookup"><span data-stu-id="7c827-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="7c827-109">Python</span><span class="sxs-lookup"><span data-stu-id="7c827-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="7c827-110">REST</span><span class="sxs-lookup"><span data-stu-id="7c827-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="7c827-111">Proveedor de recursos de REST</span><span class="sxs-lookup"><span data-stu-id="7c827-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="7c827-112">SQL</span><span class="sxs-lookup"><span data-stu-id="7c827-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="7c827-113">**Descarga del SDK**</span><span class="sxs-lookup"><span data-stu-id="7c827-113">**SDK download**</span></span></td><td>[<span data-ttu-id="7c827-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="7c827-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="7c827-115">**Documentación de la API**</span><span class="sxs-lookup"><span data-stu-id="7c827-115">**API documentation**</span></span></td><td>[<span data-ttu-id="7c827-116">Documentación de referencia de API de .NET</span><span class="sxs-lookup"><span data-stu-id="7c827-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="7c827-117">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="7c827-117">**Samples**</span></span></td><td>[<span data-ttu-id="7c827-118">Ejemplos de código de .NET</span><span class="sxs-lookup"><span data-stu-id="7c827-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="7c827-119">**Introducción**</span><span class="sxs-lookup"><span data-stu-id="7c827-119">**Get started**</span></span></td><td>[<span data-ttu-id="7c827-120">Empezar a trabajar con hello Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="7c827-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="7c827-121">**Tutorial de la aplicación web**</span><span class="sxs-lookup"><span data-stu-id="7c827-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="7c827-122">Desarrollo de aplicaciones web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7c827-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="7c827-123">**Plataforma admitida actualmente**</span><span class="sxs-lookup"><span data-stu-id="7c827-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="7c827-124">.NET Standard 1.6 y .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="7c827-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="7c827-125">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="7c827-125">Release Notes</span></span>

<span data-ttu-id="7c827-126">Hello Azure Cosmos DB .NET Core SDK tiene una paridad de características con la versión más reciente de Hola de hello [SDK de .NET de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7c827-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="7c827-127">Hello Azure Cosmos DB .NET Core SDK todavía no es compatible con aplicaciones de la plataforma Universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="7c827-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="7c827-128">Si está interesado en hello .NET Core SDK que admite las aplicaciones UWP, enviar correo electrónico demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7c827-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="7c827-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="7c827-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="7c827-130">Se agregó compatibilidad para PartitionKeyRangeId como un FeedOption para definir el ámbito de valor de intervalo de claves de consulta resultados tooa partición específica.</span><span class="sxs-lookup"><span data-stu-id="7c827-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="7c827-131">Se agregó compatibilidad para StartTime como un toostart ChangeFeedOption buscando cambios Hola después de ese tiempo.</span><span class="sxs-lookup"><span data-stu-id="7c827-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="7c827-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="7c827-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="7c827-133">Se corrigió un problema en hello clase JsonSerializable que podría provocar una excepción de desbordamiento de pila.</span><span class="sxs-lookup"><span data-stu-id="7c827-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="7c827-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="7c827-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="7c827-135">Se agregó compatibilidad con la especificación de JsonSerializerSettings personalizado al crear una instancia de [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="7c827-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="7c827-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="7c827-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="7c827-137">Se admiten 1.5 estándar de .NET como uno de los marcos de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c827-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="7c827-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="7c827-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="7c827-139">Se corrigió un problema que afectaba a las máquinas x64 que no admiten instrucciones SSE4 y que producía una excepción SEHException al ejecutar consultas de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7c827-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="7c827-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="7c827-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="7c827-141">Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="7c827-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="7c827-142">Se agregó compatibilidad con métricas de consulta para particiones individuales.</span><span class="sxs-lookup"><span data-stu-id="7c827-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="7c827-143">Se agregó compatibilidad para limitar el tamaño de Hola Hola de token de continuación para las consultas.</span><span class="sxs-lookup"><span data-stu-id="7c827-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="7c827-144">Se agregó compatibilidad para un seguimiento más detallado de las solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="7c827-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="7c827-145">Realizado algunas mejoras de rendimiento en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="7c827-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="7c827-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="7c827-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="7c827-147">Se ha corregido un problema que omite el valor de PartitionKey de hello proporcionado en FeedOptions para consultas de agregado.</span><span class="sxs-lookup"><span data-stu-id="7c827-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="7c827-148">Se ha corregido un problema en el control transparente de administración de particiones durante la ejecución entre particiones de la consulta Order By.</span><span class="sxs-lookup"><span data-stu-id="7c827-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="7c827-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="7c827-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="7c827-150">Se ha corregido un problema que provocó interbloqueos en algunos de hello async API cuando se usa dentro del contexto ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7c827-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="7c827-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="7c827-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="7c827-152">Corrige toomake SDK más resistente tooautomatic conmutación por error en determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="7c827-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="7c827-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="7c827-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="7c827-154">Corrección para un problema que en ocasiones, provoca una excepción WebException: no se pudo resolver el nombre remoto Hola.</span><span class="sxs-lookup"><span data-stu-id="7c827-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="7c827-155">Hola agregado compatibilidad para leer un documento mecanografiado directamente mediante la adición de nuevas sobrecargas tooReadDocumentAsync API.</span><span class="sxs-lookup"><span data-stu-id="7c827-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="7c827-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="7c827-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="7c827-157">Se agregó compatibilidad con consultas de agregación para LINQ (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="7c827-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="7c827-158">Corregir un problema de pérdida de memoria para el objeto de ConnectionPolicy Hola causado por el uso de Hola de controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="7c827-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="7c827-159">Se corrigió un problema por el que UpsertAttachmentAsync no funcionaba cuando se usaba el valor ETag.</span><span class="sxs-lookup"><span data-stu-id="7c827-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="7c827-160">Se corrigió un problema por el que la continuación de la consulta order-by en la partición cruzada no funcionaba cuando se ordenaba por un campo de cadena.</span><span class="sxs-lookup"><span data-stu-id="7c827-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="7c827-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="7c827-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="7c827-162">Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG).</span><span class="sxs-lookup"><span data-stu-id="7c827-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="7c827-163">Consulte [Compatibilidad con agregación](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="7c827-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="7c827-164">Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="7c827-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="7c827-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="7c827-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="7c827-166">Hello Azure Cosmos DB .NET Core SDK permite toobuild rápidos, multiplataforma [ASP.NET Core](https://www.asp.net/core) y [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicaciones en Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="7c827-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="7c827-167">Hola versión más reciente de hello Azure Cosmos DB .NET Core SDK es totalmente [Xamarin](https://www.xamarin.com) compatible y aplicaciones usados toobuild destinados a iOS, Android y Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="7c827-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="7c827-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="7c827-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="7c827-169">Hola SDK de vista previa de Azure Cosmos DB .NET Core le permite toobuild rápidos, multiplataforma [ASP.NET Core](https://www.asp.net/core) y [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicaciones en Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="7c827-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="7c827-170">Hola SDK de Azure Cosmos DB .NET Core Preview tiene una paridad de características con la versión más reciente de Hola de hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) y es compatible con hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="7c827-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="7c827-171">Todos los [modos de conexión](performance-tips.md#networking): modo de puerta de enlace, TCP directo y HTTPS directo.</span><span class="sxs-lookup"><span data-stu-id="7c827-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="7c827-172">Todos los [niveles de coherencia](consistency-levels.md): fuerte, sesión, obsolescencia limitada y ocasional.</span><span class="sxs-lookup"><span data-stu-id="7c827-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="7c827-173">[Colecciones con particiones](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="7c827-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="7c827-174">[Cuentas de base de datos de varias regiones y replicación geográfica](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="7c827-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="7c827-175">Si tiene preguntas relacionadas toothis SDK, registrar demasiado[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), archivo o un problema en hello [repositorio de github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="7c827-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="7c827-176">Fechas de lanzamiento y de retirada</span><span class="sxs-lookup"><span data-stu-id="7c827-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="7c827-177">Versión</span><span class="sxs-lookup"><span data-stu-id="7c827-177">Version</span></span> | <span data-ttu-id="7c827-178">Fecha de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="7c827-178">Release Date</span></span> | <span data-ttu-id="7c827-179">Fecha de retirada</span><span class="sxs-lookup"><span data-stu-id="7c827-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="7c827-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="7c827-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="7c827-181">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="7c827-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="7c827-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="7c827-183">7 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="7c827-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="7c827-185">2 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="7c827-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="7c827-187">12 de junio de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="7c827-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="7c827-189">23 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="7c827-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="7c827-191">10 de mayo de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="7c827-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="7c827-193">19 de abril de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="7c827-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="7c827-195">29 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="7c827-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="7c827-197">25 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="7c827-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="7c827-199">20 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="7c827-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="7c827-201">14 de marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="7c827-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="7c827-203">16 de febrero de 2017</span><span class="sxs-lookup"><span data-stu-id="7c827-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="7c827-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="7c827-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="7c827-205">21 de diciembre de 2016</span><span class="sxs-lookup"><span data-stu-id="7c827-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="7c827-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="7c827-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="7c827-207">15 de noviembre de 2016</span><span class="sxs-lookup"><span data-stu-id="7c827-207">November 15, 2016</span></span> |<span data-ttu-id="7c827-208">31 de diciembre de 2016</span><span class="sxs-lookup"><span data-stu-id="7c827-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="7c827-209">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7c827-209">See Also</span></span>
<span data-ttu-id="7c827-210">toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.</span><span class="sxs-lookup"><span data-stu-id="7c827-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

