---
title: API de tabla de DB aaaIntroduction tooAzure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede utilizar la base de datos de Azure Cosmos toostore y populares OSS MongoDB APIs de Hola de grandes volúmenes de datos de clave y valor con el uso de baja latencia de consulta."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a><span data-ttu-id="1a87e-103">Introducción tooAzure DB Cosmos: API de tabla</span><span class="sxs-lookup"><span data-stu-id="1a87e-103">Introduction tooAzure Cosmos DB: Table API</span></span>

<span data-ttu-id="1a87e-104">[Azure Cosmos DB](introduction.md) es un servicio de base de datos con varios modelos y distribución global de Microsoft para aplicaciones críticas.</span><span class="sxs-lookup"><span data-stu-id="1a87e-104">[Azure Cosmos DB](introduction.md) is Microsoft's globally distributed, multi-model database service for mission-critical applications.</span></span> <span data-ttu-id="1a87e-105">Proporciona la base de datos de Azure Cosmos [distribución global preparada](distribute-data-globally.md), [escalado flexible de rendimiento y almacenamiento](partition-data.md) latencias de milisegundo en todo el mundo, solo dígito se escriben en el percentil 99 de hello, [cinco niveles de coherencia bien definido](consistency-levels.md)y garantiza la alta disponibilidad, todo ello respaldado por [líderes en la industria SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1a87e-105">Azure Cosmos DB provides [turn-key global distribution](distribute-data-globally.md), [elastic scaling of throughput and storage](partition-data.md) worldwide, single-digit millisecond latencies at hello 99th percentile, [five well-defined consistency levels](consistency-levels.md), and guaranteed high availability, all backed by [industry-leading SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/).</span></span> <span data-ttu-id="1a87e-106">Base de datos de Azure Cosmos [automáticamente los datos de índices](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sin necesidad de toodeal con administración de esquema y de índice.</span><span class="sxs-lookup"><span data-stu-id="1a87e-106">Azure Cosmos DB [automatically indexes data](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) without requiring you toodeal with schema and index management.</span></span> <span data-ttu-id="1a87e-107">Sigue varios modelos y es compatible con los modelos de datos de documento, de clave-valor, de grafo y de columnas.</span><span class="sxs-lookup"><span data-stu-id="1a87e-107">It is multi-model and supports document, key-value, graph, and columnar data models.</span></span> 

![API Table Storage de Azure y Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

<span data-ttu-id="1a87e-109">Base de datos de Azure Cosmos proporciona Hola API (vista previa) de la tabla para las aplicaciones que necesitan un almacén de clave y valor con esquema flexible, un rendimiento predecible, distribución global y un alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1a87e-109">Azure Cosmos DB provides hello Table API (preview) for applications that need a key-value store with flexible schema, predictable performance, global distribution, and high throughput.</span></span> <span data-ttu-id="1a87e-110">Hola API de tabla proporciona Hola misma funcionalidad que el almacenamiento de tabla de Azure, pero aprovecha todos los beneficios de Hola de motor de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="1a87e-110">hello Table API provides hello same functionality as Azure Table storage, but leverages hello benefits of hello Azure Cosmos DB engine.</span></span> 

<span data-ttu-id="1a87e-111">Puede continuar toouse almacenamiento de tabla de Azure para las tablas con almacenamiento alta y requisitos de rendimiento inferior.</span><span class="sxs-lookup"><span data-stu-id="1a87e-111">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="1a87e-112">Azure DB Cosmos incorporará la compatibilidad con tablas con optimización para el almacenamiento en una futura actualización y se actualiza la tabla de Azure nuevas y existentes serán las cuentas de almacenamiento tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a87e-112">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be upgraded tooAzure Cosmos DB.</span></span>

## <a name="premium-and-standard-table-apis"></a><span data-ttu-id="1a87e-113">API Table premium y estándar</span><span class="sxs-lookup"><span data-stu-id="1a87e-113">Premium and standard Table APIs</span></span>
<span data-ttu-id="1a87e-114">Si actualmente usa almacenamiento de tabla de Azure, obtendrá Hola después ventajas moviendo "premium" vista previa de DB tooAzure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="1a87e-114">If you currently use Azure Table storage, you gain hello following benefits by moving tooAzure Cosmos DB's "premium table" preview:</span></span>

|  | <span data-ttu-id="1a87e-115">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="1a87e-115">Azure Table Storage</span></span> | <span data-ttu-id="1a87e-116">Table Storage de Azure Cosmos DB (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="1a87e-116">Azure Cosmos DB: Table storage (preview)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a87e-117">Latency</span><span class="sxs-lookup"><span data-stu-id="1a87e-117">Latency</span></span> | <span data-ttu-id="1a87e-118">Rápido, pero no hay límites máximos en la latencia.</span><span class="sxs-lookup"><span data-stu-id="1a87e-118">Fast, but no upper bounds on latency</span></span> | <span data-ttu-id="1a87e-119">Con el respaldo de latencia de milisegundos de un solo dígito para lecturas y escrituras, < 10 ms de latencia lee y < 15 ms de latencia se escribe en el percentil 99 de hello, en cualquiera de ellas, en cualquier lugar de Hola a todos</span><span class="sxs-lookup"><span data-stu-id="1a87e-119">Single-digit millisecond latency for reads and writes, backed with <10 ms latency reads and <15 ms latency writes at hello 99th percentile, at any scale, anywhere in hello world</span></span> |
| <span data-ttu-id="1a87e-120">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="1a87e-120">Throughput</span></span> | <span data-ttu-id="1a87e-121">Altamente escalable, pero sin un modelo de rendimiento dedicado.</span><span class="sxs-lookup"><span data-stu-id="1a87e-121">Highly scalable, but no dedicated throughput model.</span></span> <span data-ttu-id="1a87e-122">Las tablas tienen un límite de escalabilidad de 20 000 operaciones por segundo.</span><span class="sxs-lookup"><span data-stu-id="1a87e-122">Tables have a scalability limit of 20,000 operations/s</span></span> | <span data-ttu-id="1a87e-123">Altamente escalable con [rendimiento reservado dedicado por tabla](request-units.md), respaldado por el SLA.</span><span class="sxs-lookup"><span data-stu-id="1a87e-123">Highly scalable with [dedicated reserved throughput per table](request-units.md), that is backed by SLAs.</span></span> <span data-ttu-id="1a87e-124">Las cuentas no tienen límite máximo en el rendimiento y admiten más de 10 millones de operaciones por segundo por tabla.</span><span class="sxs-lookup"><span data-stu-id="1a87e-124">Accounts have no upper limit on throughput, and support >10 million operations/s per table</span></span> |
| <span data-ttu-id="1a87e-125">Distribución global</span><span class="sxs-lookup"><span data-stu-id="1a87e-125">Global Distribution</span></span> | <span data-ttu-id="1a87e-126">Una sola región, con una región de lectura secundaria legible opcional para alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="1a87e-126">Single region with one optional readable secondary read region for HA.</span></span> <span data-ttu-id="1a87e-127">No se puede iniciar la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1a87e-127">You cannot initiate failover</span></span> | <span data-ttu-id="1a87e-128">[Distribución global preparada](distribute-data-globally.md) desde una too30 + regiones, soporte para [conmutaciones por error automática y manual](regional-failover.md) en cualquier momento, en cualquier lugar de Hola a todos</span><span class="sxs-lookup"><span data-stu-id="1a87e-128">[Turn-key global distribution](distribute-data-globally.md) from one too30+ regions, Support for [automatic and manual failovers](regional-failover.md) at any time, anywhere in hello world</span></span> |
| <span data-ttu-id="1a87e-129">Indización</span><span class="sxs-lookup"><span data-stu-id="1a87e-129">Indexing</span></span> | <span data-ttu-id="1a87e-130">Índice principal solo en PartitionKey y RowKey.</span><span class="sxs-lookup"><span data-stu-id="1a87e-130">Only primary index on PartitionKey and RowKey.</span></span> <span data-ttu-id="1a87e-131">No hay índices secundarios.</span><span class="sxs-lookup"><span data-stu-id="1a87e-131">No secondary indexes</span></span> | <span data-ttu-id="1a87e-132">Indexación automática y completa en todas las propiedades, sin administración de índices.</span><span class="sxs-lookup"><span data-stu-id="1a87e-132">Automatic and complete indexing on all properties, no index management</span></span> |
| <span data-ttu-id="1a87e-133">Consultar</span><span class="sxs-lookup"><span data-stu-id="1a87e-133">Query</span></span> | <span data-ttu-id="1a87e-134">La ejecución de consultas usa el índice de la clave principal y, en caso contrario, examina.</span><span class="sxs-lookup"><span data-stu-id="1a87e-134">Query execution uses index for primary key, and scans otherwise.</span></span> | <span data-ttu-id="1a87e-135">Las consultas pueden aprovechar la indexación automática en las propiedades para reducir el tiempo de consulta.</span><span class="sxs-lookup"><span data-stu-id="1a87e-135">Queries can take advantage of automatic indexing on properties for fast query times.</span></span> <span data-ttu-id="1a87e-136">El motor de base de datos de Azure Cosmos DB puede admitir agregados, funciones geoespaciales y ordenación.</span><span class="sxs-lookup"><span data-stu-id="1a87e-136">Azure Cosmos DB's database engine is capable of supporting aggregates, geo-spatial, and sorting.</span></span> |
| <span data-ttu-id="1a87e-137">Coherencia</span><span class="sxs-lookup"><span data-stu-id="1a87e-137">Consistency</span></span> | <span data-ttu-id="1a87e-138">Fuerte en la región primaria, Final en la región secundaria.</span><span class="sxs-lookup"><span data-stu-id="1a87e-138">Strong within primary region, Eventual with secondary region</span></span> | <span data-ttu-id="1a87e-139">[Cinco niveles de coherencia bien definido](consistency-levels.md) tootrade desactivar disponibilidad, latencia, el rendimiento y coherencia según sus necesidades de aplicación</span><span class="sxs-lookup"><span data-stu-id="1a87e-139">[Five well-defined consistency levels](consistency-levels.md) tootrade off availability, latency, throughput, and consistency based on your application needs</span></span> |
| <span data-ttu-id="1a87e-140">Precios</span><span class="sxs-lookup"><span data-stu-id="1a87e-140">Pricing</span></span> | <span data-ttu-id="1a87e-141">Optimizado para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1a87e-141">Storage-optimized</span></span>  | <span data-ttu-id="1a87e-142">Optimizado para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1a87e-142">Throughput-optimized</span></span> |
| <span data-ttu-id="1a87e-143">SLA</span><span class="sxs-lookup"><span data-stu-id="1a87e-143">SLAs</span></span> | <span data-ttu-id="1a87e-144">Disponibilidad del 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="1a87e-144">99.9% availability</span></span> | <span data-ttu-id="1a87e-145">disponibilidad del 99,99% dentro de una única región y capacidad tooadd más regiones para una mayor disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="1a87e-145">99.99% availability within a single region, and ability tooadd more regions for higher availability.</span></span> <span data-ttu-id="1a87e-146">[SLA completos líderes en el sector](https://azure.microsoft.com/support/legal/sla/cosmos-db/) en disponibilidad general.</span><span class="sxs-lookup"><span data-stu-id="1a87e-146">[Industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span> |

## <a name="how-tooget-started"></a><span data-ttu-id="1a87e-147">Cómo iniciar tooget</span><span class="sxs-lookup"><span data-stu-id="1a87e-147">How tooget started</span></span>

<span data-ttu-id="1a87e-148">Crear una cuenta de base de datos de Azure Cosmos en hello [portal de Azure](https://portal.azure.com)y empezar a trabajar con nuestro [inicio rápido para API de tabla mediante .NET](create-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1a87e-148">Create an Azure Cosmos DB account in hello [Azure portal](https://portal.azure.com), and get started with our [Quickstart for Table API using .NET](create-table-dotnet.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1a87e-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a87e-149">Next steps</span></span>

<span data-ttu-id="1a87e-150">A continuación, presentamos unos tooget punteros se inició:</span><span class="sxs-lookup"><span data-stu-id="1a87e-150">Here are a few pointers tooget you started:</span></span>
* [<span data-ttu-id="1a87e-151">Compilar una aplicación de .NET mediante Hola API de tabla</span><span class="sxs-lookup"><span data-stu-id="1a87e-151">Build a .NET application using hello Table API</span></span>](create-table-dotnet.md)
* [<span data-ttu-id="1a87e-152">Desarrollar con hello API de tabla en .NET</span><span class="sxs-lookup"><span data-stu-id="1a87e-152">Develop with hello Table API in .NET</span></span>](tutorial-develop-table-dotnet.md)
* [<span data-ttu-id="1a87e-153">Datos de la tabla de consulta mediante el uso de hello API de tabla</span><span class="sxs-lookup"><span data-stu-id="1a87e-153">Query table data by using hello Table API</span></span>](tutorial-query-table.md)
* [<span data-ttu-id="1a87e-154">Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de tabla</span><span class="sxs-lookup"><span data-stu-id="1a87e-154">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>](tutorial-global-distribution-table.md)
* [<span data-ttu-id="1a87e-155">Table API .NET de Azure Cosmos DB: descarga y notas de la versión</span><span class="sxs-lookup"><span data-stu-id="1a87e-155">Azure Cosmos DB Table API SDK for .NET</span></span>](table-sdk-dotnet.md)