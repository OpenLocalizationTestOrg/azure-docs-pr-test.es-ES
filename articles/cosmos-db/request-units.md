---
title: aaaRequest unidades & calcular rendimiento - base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo especificar toounderstand y estimar los requisitos de la unidad de solicitud en la base de datos de Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="63b9a-103">Unidades de solicitud en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="63b9a-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="63b9a-104">Ya disponible: la [calculadora de unidades de solicitud](https://www.documentdb.com/capacityplanner) de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="63b9a-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="63b9a-105">Obtenga más información en [Estimación de las necesidades de rendimiento](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="63b9a-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Calculadora de rendimiento][5]

## <a name="introduction"></a><span data-ttu-id="63b9a-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="63b9a-107">Introduction</span></span>
<span data-ttu-id="63b9a-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="63b9a-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="63b9a-109">Con la base de datos de Azure Cosmos, no tiene máquinas virtuales que toorent, implementar software o supervisar las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="63b9a-110">Base de datos de Azure Cosmos se opera y continuamente supervisado por Microsoft ingenieros superior toodeliver world clase disponibilidad, rendimiento y protección de datos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="63b9a-111">Puede acceder a sus datos con las API de su preferencia, como [DocumentDB SQL](documentdb-sql-query.md) (documentos), MongoDB (documentos), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (clave-valor) y [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafos), que admite de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="63b9a-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="63b9a-112">moneda Hola de base de datos de Azure Cosmos es hello unidad de solicitud (RU).</span><span class="sxs-lookup"><span data-stu-id="63b9a-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="63b9a-113">Con RUs, no es necesario tooreserve capacidades de lectura/escritura o aprovisionar CPU, memoria y e/s por segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="63b9a-114">Base de datos de Azure Cosmos es compatible con una serie de interfaces API con diferentes operaciones comprendido entre lecturas simples y escribe toocomplex consultas de gráfico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="63b9a-115">Puesto que no todas las solicitudes son iguales, se asignan una cantidad normalizada de **unidades de solicitud** según la cantidad de Hola de solicitud de cálculo necesarios tooserve Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="63b9a-116">número de Hola de unidades de solicitud para una operación es determinista y puede realizar un seguimiento de número de Hola de unidades de solicitud consumidas por cualquier operación en la base de datos de Azure Cosmos a través de un encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="63b9a-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="63b9a-117">tooprovide un rendimiento predecible, es necesario tooreserve rendimiento en unidades de 100 RU/segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="63b9a-118">Después de leer este artículo, podrá hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="63b9a-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="63b9a-119">¿Qué son las unidades de solicitud y los cargos de solicitud?</span><span class="sxs-lookup"><span data-stu-id="63b9a-119">What are request units and request charges?</span></span>
* <span data-ttu-id="63b9a-120">¿Cómo se puede especificar la capacidad de unidad de solicitud para una colección?</span><span class="sxs-lookup"><span data-stu-id="63b9a-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="63b9a-121">¿Cómo puedo estimar mis necesidades de unidad de solicitud de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="63b9a-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="63b9a-122">¿Qué ocurre si supero la capacidad de la unidad de solicitud para una colección?</span><span class="sxs-lookup"><span data-stu-id="63b9a-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="63b9a-123">Base de datos de Azure Cosmos sea una base de datos de varios modelo, es importante toonote que nos referiremos tooa colección/documento de un documento de API, un nodo de gráfico/para una API de graph y una tabla o entidad para la API de la tabla.</span><span class="sxs-lookup"><span data-stu-id="63b9a-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="63b9a-124">Rendimiento de este documento se generalizará toohello conceptos de contenedor de elementos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="63b9a-125">Unidades de solicitud y cargos de solicitud</span><span class="sxs-lookup"><span data-stu-id="63b9a-125">Request units and request charges</span></span>
<span data-ttu-id="63b9a-126">Base de datos de Cosmos Azure ofrece un rendimiento rápido y predecible por *reservar* necesidades de rendimiento de la aplicación de recursos toosatisfy.</span><span class="sxs-lookup"><span data-stu-id="63b9a-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="63b9a-127">Como aplicación de carga y patrones de acceso cambian con el tiempo, base de datos de Azure Cosmos permite tooeasily aumentar o reducir Hola de aplicación tooyour disponible de rendimiento reservados.</span><span class="sxs-lookup"><span data-stu-id="63b9a-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="63b9a-128">Con Azure Cosmos DB, el rendimiento reservado se especifica en términos de procesamiento de unidades de solicitud por segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="63b9a-129">Se puede considerar de unidades de solicitud como moneda de rendimiento, mediante el cual se *reservar* garantiza que una cantidad de unidades de solicitud aplicación tooyour disponible en por segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="63b9a-130">Cada operación de Azure Cosmos DB: escritura de un documento, realización de una consulta, actualización de un documento, consume CPU, memoria y E/S por segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="63b9a-131">Es decir, cada operación implica un *cargo de solicitud*, que se expresa en *unidades de solicitud*.</span><span class="sxs-lookup"><span data-stu-id="63b9a-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="63b9a-132">Descripción de los factores de Hola que afectan a los cargos de unidad de solicitud, junto con los requisitos de rendimiento de su aplicación, permite que se toorun la aplicación como costo eficazmente como sea posible.</span><span class="sxs-lookup"><span data-stu-id="63b9a-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="63b9a-133">Explorador de consulta de Hello es también una maravillosa herramienta tootest Hola de principales de una consulta.</span><span class="sxs-lookup"><span data-stu-id="63b9a-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="63b9a-134">Se recomienda introducción, inspeccionando Hola después de vídeo, donde se explica Aravind Ramachandran unidades de solicitud y un rendimiento predecible con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="63b9a-135">Especificación de la capacidad de unidad de solicitud en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="63b9a-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="63b9a-136">Al iniciar una nueva colección, tabla o gráfico, especifique el número de Hola de unidades de solicitud por segundo (RU por segundo) que desea reservada.</span><span class="sxs-lookup"><span data-stu-id="63b9a-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="63b9a-137">En función de rendimiento aprovisionado hello, base de datos de Azure Cosmos asigna toohost de particiones físicas en la colección y divisiones/rebalancea datos entre particiones cuando crece.</span><span class="sxs-lookup"><span data-stu-id="63b9a-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="63b9a-138">Base de datos de Azure Cosmos requiere que un toobe de clave de partición especificado cuando una colección está aprovisionado con 2.500 unidades de solicitud o superior.</span><span class="sxs-lookup"><span data-stu-id="63b9a-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="63b9a-139">Una clave de partición también es necesario tooscale el rendimiento de la colección más allá de 2.500 unidades de solicitud en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="63b9a-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="63b9a-140">Por lo tanto, se recomienda encarecidamente tooconfigure una [clave de partición](partition-data.md) al crear un contenedor, independientemente de su rendimiento inicial.</span><span class="sxs-lookup"><span data-stu-id="63b9a-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="63b9a-141">Dado que los datos podrían tener toobe dividir en varias particiones, es necesario toopick una clave de partición que tenga una cardinalidad alta (100 toomillions de valores distintos) para que la colección, tabla o gráfico y las solicitudes se pueden escalar uniformemente por base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="63b9a-142">Una clave de partición es un límite lógico, no uno físico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="63b9a-143">Por lo tanto, no es necesario el número de hello toolimit de valores de clave de partición distintos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="63b9a-144">De hecho es mejor toohave mayor que menor, los valores de clave de partición como base de datos de Azure Cosmos tiene más opciones de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="63b9a-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="63b9a-145">Este es un fragmento de código para crear una colección con 3.000 solicitud unidades por segundo mediante Hola .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="63b9a-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="63b9a-146">Azure Cosmos DB funciona con un modelo de reserva del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="63b9a-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="63b9a-147">Es decir, se le cobra según cantidad Hola de rendimiento *reservada*, independientemente de la cantidad de ese rendimiento está activamente *utiliza*.</span><span class="sxs-lookup"><span data-stu-id="63b9a-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="63b9a-148">Como carga, datos y el uso cambien los patrones la aplicación puede escalar fácilmente arriba y abajo Hola cantidad de RUs reservadas mediante SDK o con hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63b9a-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="63b9a-149">Se asignan a cada colección, tabla o gráfico tooan `Offer` recursos en Azure Cosmos DB, que contiene los metadatos sobre el rendimiento aprovisionado Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="63b9a-150">Puede cambiar rendimiento Hola asignada, búsqueda de recurso de oferta correspondiente de Hola para un contenedor y actualizarla con el nuevo valor de rendimiento Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="63b9a-151">Este es un fragmento de código para cambiar el rendimiento de una colección too5 hello, 000 unidades de solicitud por segundo con Hola .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="63b9a-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="63b9a-152">Cuando se cambia el rendimiento de hello, hay sin disponibilidad de toohello del impacto del contenedor.</span><span class="sxs-lookup"><span data-stu-id="63b9a-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="63b9a-153">Rendimiento reservadas nuevas Hola suele ser eficaz en segundos en la aplicación de rendimiento nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="63b9a-154">Consideraciones de la unidad de solicitud</span><span class="sxs-lookup"><span data-stu-id="63b9a-154">Request unit considerations</span></span>
<span data-ttu-id="63b9a-155">Al calcular el número de Hola de tooreserve de unidades de solicitud para el contenedor de la base de datos de Azure Cosmos, es hello tootake importante después de las variables en cuenta:</span><span class="sxs-lookup"><span data-stu-id="63b9a-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="63b9a-156">**Tamaño del elemento**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-156">**Item size**.</span></span> <span data-ttu-id="63b9a-157">Como tamaño aumenta Hola unidades consumidas tooread o escribir datos de hello también aumentará.</span><span class="sxs-lookup"><span data-stu-id="63b9a-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="63b9a-158">**Recuento de propiedades del elemento**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-158">**Item property count**.</span></span> <span data-ttu-id="63b9a-159">Suponiendo que de forma predeterminada la indización de todas las propiedades, Hola unidades consumidas toowrite un documento, nodo/ntity aumentará como Hola propiedad recuento aumenta.</span><span class="sxs-lookup"><span data-stu-id="63b9a-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="63b9a-160">**Coherencia de datos**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-160">**Data consistency**.</span></span> <span data-ttu-id="63b9a-161">Cuando se usa niveles de coherencia de datos de Strong o Bounded Staleness, unidades adicionales será consumido tooread elementos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="63b9a-162">**Propiedades indexadas**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-162">**Indexed properties**.</span></span> <span data-ttu-id="63b9a-163">Una directiva de índice en cada contenedor determina qué propiedades se indexan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="63b9a-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="63b9a-164">Puede reducir el consumo de unidades de solicitud limitando el número de Hola de las propiedades indizadas o habilitando la indexación diferida.</span><span class="sxs-lookup"><span data-stu-id="63b9a-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="63b9a-165">**Indexación de documentos**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-165">**Document indexing**.</span></span> <span data-ttu-id="63b9a-166">De forma predeterminada, que cada elemento se indiza automáticamente, consumirá menos unidades de solicitud si elige no tooindex algunos de los elementos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="63b9a-167">**Patrones de consultas**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-167">**Query patterns**.</span></span> <span data-ttu-id="63b9a-168">complejidad de Hola de una consulta afecta a cuántas unidades de solicitud se usan para una operación.</span><span class="sxs-lookup"><span data-stu-id="63b9a-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="63b9a-169">número de Hola de predicados, naturaleza de los predicados de hello, proyecciones, número de UDF y el tamaño de hello del conjunto de datos de origen de hello todos influyen en el costo de Hola de operaciones de consulta.</span><span class="sxs-lookup"><span data-stu-id="63b9a-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="63b9a-170">**Uso de script**.</span><span class="sxs-lookup"><span data-stu-id="63b9a-170">**Script usage**.</span></span>  <span data-ttu-id="63b9a-171">Al igual que con las consultas, procedimientos almacenados y desencadenadores consumen unidades de solicitud basándose en hello complejidad de las operaciones de Hola que se está realizando.</span><span class="sxs-lookup"><span data-stu-id="63b9a-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="63b9a-172">Al desarrollar la aplicación, inspeccionar el cargo de la solicitud de hello toobetter encabezado entender cómo cada operación consume una capacidad de unidad de solicitud.</span><span class="sxs-lookup"><span data-stu-id="63b9a-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="63b9a-173">Estimación de necesidades de rendimiento</span><span class="sxs-lookup"><span data-stu-id="63b9a-173">Estimating throughput needs</span></span>
<span data-ttu-id="63b9a-174">Una unidad de solicitud es una medida normalizada del costo de procesamiento de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="63b9a-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="63b9a-175">Una unidad única solicitud representa Hola procesamiento capacidad requerida tooread (a través de vínculos propios o Id. de) un elemento que se compone de 10 valores de la propiedad unique (excepto las propiedades del sistema) de 1KB único.</span><span class="sxs-lookup"><span data-stu-id="63b9a-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="63b9a-176">Un toocreate de solicitud (insert), reemplazar o eliminar Hola mismo elemento consumirá más capacidad de procesamiento del servicio de hello y, por tanto, más unidades de solicitud.</span><span class="sxs-lookup"><span data-stu-id="63b9a-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="63b9a-177">línea de base de Hola de unidad 1 solicitud para un 1KB elemento corresponde tooa simple obtener por Id. de elemento de Hola o vínculo propio.</span><span class="sxs-lookup"><span data-stu-id="63b9a-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="63b9a-178">Por ejemplo, aquí es una tabla que muestra cuántos solicitar unidades tooprovision en tres tamaños de los distintos elementos (1KB, 4KB y 64KB) y en dos niveles de rendimiento diferentes (500 lecturas por segundo 100 escrituras por segundo y 500 lecturas por segundo + 500 escrituras por segundo).</span><span class="sxs-lookup"><span data-stu-id="63b9a-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="63b9a-179">coherencia de los datos Hola se configuró en la sesión y Hola directiva de indexación se estableció tooNone.</span><span class="sxs-lookup"><span data-stu-id="63b9a-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-180"><strong>Tamaño del elemento</strong></span><span class="sxs-lookup"><span data-stu-id="63b9a-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-181"><strong>Lecturas/segundo</strong></span><span class="sxs-lookup"><span data-stu-id="63b9a-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-182"><strong>Escrituras/segundo</strong></span><span class="sxs-lookup"><span data-stu-id="63b9a-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-183"><strong>Unidades de solicitud</strong></span><span class="sxs-lookup"><span data-stu-id="63b9a-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="63b9a-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-185">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-186">100</span><span class="sxs-lookup"><span data-stu-id="63b9a-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-187">(500 * 1) + (100 * 5) = 1000 RU/s</span><span class="sxs-lookup"><span data-stu-id="63b9a-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="63b9a-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-189">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-190">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-191">(500 * 1) + (500 * 5) = 3000 RU/s</span><span class="sxs-lookup"><span data-stu-id="63b9a-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="63b9a-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-193">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-194">100</span><span class="sxs-lookup"><span data-stu-id="63b9a-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-195">(500 * 1,3) + (100 * 7) = 1350 RU/s</span><span class="sxs-lookup"><span data-stu-id="63b9a-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="63b9a-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-197">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-198">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-199">(500 * 1,3) + (500 * 7) = 4150 RU/s</span><span class="sxs-lookup"><span data-stu-id="63b9a-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="63b9a-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-201">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-202">100</span><span class="sxs-lookup"><span data-stu-id="63b9a-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-203">(500 * 10) + (100 * 48) = 9800 RU/s</span><span class="sxs-lookup"><span data-stu-id="63b9a-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="63b9a-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="63b9a-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-205">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-206">500</span><span class="sxs-lookup"><span data-stu-id="63b9a-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="63b9a-207">(500 * 10) + (500 * 48) = 29 000 RU/s</span><span class="sxs-lookup"><span data-stu-id="63b9a-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="63b9a-208">Usar la calculadora de unidades de solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="63b9a-208">Use hello request unit calculator</span></span>
<span data-ttu-id="63b9a-209">clientes toohelp bien optimizar sus estimaciones de rendimiento, no hay una basada en web [Calculadora de unidades de solicitud](https://www.documentdb.com/capacityplanner) toohelp estimación Hola solicitud requisitos de la unidad para las operaciones típicas, incluidos:</span><span class="sxs-lookup"><span data-stu-id="63b9a-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="63b9a-210">Creaciones (escrituras) de elementos</span><span class="sxs-lookup"><span data-stu-id="63b9a-210">Item creates (writes)</span></span>
* <span data-ttu-id="63b9a-211">Lecturas de elementos</span><span class="sxs-lookup"><span data-stu-id="63b9a-211">Item reads</span></span>
* <span data-ttu-id="63b9a-212">Eliminaciones de elementos</span><span class="sxs-lookup"><span data-stu-id="63b9a-212">Item deletes</span></span>
* <span data-ttu-id="63b9a-213">Actualizaciones de elementos</span><span class="sxs-lookup"><span data-stu-id="63b9a-213">Item updates</span></span>

<span data-ttu-id="63b9a-214">herramienta de Hello también incluye compatibilidad para calcular las necesidades de almacenamiento de datos basadas en los elementos de ejemplo de Hola que proporcione.</span><span class="sxs-lookup"><span data-stu-id="63b9a-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="63b9a-215">Uso de herramienta de hello es simple:</span><span class="sxs-lookup"><span data-stu-id="63b9a-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="63b9a-216">Cargue uno o más elementos representativos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-216">Upload one or more representative items.</span></span>
   
    ![Cargar la calculadora de unidades de solicitud de elementos toohello][2]
2. <span data-ttu-id="63b9a-218">requisitos de almacenamiento de datos de tooestimate, escriba el número total de Hola de elementos esperados toostore.</span><span class="sxs-lookup"><span data-stu-id="63b9a-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="63b9a-219">Introducir número de Hola de elementos de crear, leer, actualizar y eliminar operaciones requieren (de forma por segundo).</span><span class="sxs-lookup"><span data-stu-id="63b9a-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="63b9a-220">cargos de unidad de solicitud tooestimate Hola de operaciones de actualización del elemento, cargar una copia del elemento de ejemplo de Hola del paso 1 anterior que incluye actualizaciones de campo típico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="63b9a-221">Por ejemplo, si las actualizaciones de elementos normalmente modificar dos propiedades denominadas lastLogin y userVisits y, a continuación, basta con copiar el elemento de ejemplo de Hola, actualice los valores de hello de esas dos propiedades y cargar Hola copiar elemento.</span><span class="sxs-lookup"><span data-stu-id="63b9a-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Especificar los requisitos de rendimiento de la calculadora de unidad de solicitud de Hola][3]
4. <span data-ttu-id="63b9a-223">Haga clic en calcular y examinar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-223">Click calculate and examine hello results.</span></span>
   
    ![Resultados de la calculadora de unidades de solicitud][4]

> [!NOTE]
> <span data-ttu-id="63b9a-225">Si tiene tipos de elemento que variarán considerablemente en cuanto al número de hello y tamaño de las propiedades indizadas, a continuación, cargar una muestra de cada *tipo* de toohello elemento típico de herramientas y, a continuación, calcular los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="63b9a-226">Usar el encabezado de respuesta de cargo de solicitud de base de datos de Azure Cosmos de Hola</span><span class="sxs-lookup"><span data-stu-id="63b9a-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="63b9a-227">Cada respuesta de servicio de base de datos de Azure Cosmos Hola incluye un encabezado personalizado (`x-ms-request-charge`) que contiene unidades de solicitud de hello utilizados para la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="63b9a-228">Este encabezado también es accesible a través de hello Azure Cosmos DB SDK.</span><span class="sxs-lookup"><span data-stu-id="63b9a-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="63b9a-229">Hola .NET SDK, RequestCharge es una propiedad del objeto de ResourceResponse Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="63b9a-230">Para las consultas, Hola Explorador de consulta de base de datos de Azure Cosmos Hola portal de Azure proporciona información acerca de cargos de solicitud para las consultas ejecutadas.</span><span class="sxs-lookup"><span data-stu-id="63b9a-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Examen de cargos RU Hola Explorador de consulta][1]

<span data-ttu-id="63b9a-232">Con esto en mente, un método para calcular la cantidad de Hola de rendimiento reservados requerido por la aplicación es cargo por unidad toorecord Hola solicitud asociado con la ejecución de las operaciones típicas con un elemento representativo utilizado por la aplicación y, a continuación, calcular el número de Hola de operaciones es posible anticipar realizar cada segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="63b9a-233">Ser toomeasure seguro e incluyen las consultas habituales y uso de scripts de base de datos de Azure Cosmos así.</span><span class="sxs-lookup"><span data-stu-id="63b9a-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="63b9a-234">Si tiene tipos de elemento que variarán considerablemente en cuanto al número de hello y tamaño de las propiedades indizadas, a continuación, registre el cargo por unidad Hola operación aplicable solicitud asociada a cada uno *tipo* de elemento típico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="63b9a-235">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="63b9a-235">For example:</span></span>

1. <span data-ttu-id="63b9a-236">Registrar Hola cargo de unidad de solicitud de creación (Insertar) un elemento típico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="63b9a-237">Cargos de unidad de solicitud de registro Hola de leer un elemento típico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="63b9a-238">Cargos de unidad de registro Hola solicitud de actualización de un elemento típico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="63b9a-239">Cargos de unidad de solicitud Hola registro de consultas de elemento típicas, comunes.</span><span class="sxs-lookup"><span data-stu-id="63b9a-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="63b9a-240">Cargo de unidad de solicitud de hello registros de los scripts personalizados (procedimientos almacenados, desencadenadores, funciones definidas por el usuario) usado por la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="63b9a-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="63b9a-241">Calcular la solicitud requiere Hola que unidades dados Hola estimado número de operaciones prevé toorun cada segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="63b9a-242"><a id="GetLastRequestStatistics"></a>Uso del comando GetLastRequestStatistics de la API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="63b9a-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="63b9a-243">API de MongoDB admite un comando personalizado, *getLastRequestStatistics*, para recuperar el cargo de la solicitud de Hola para operaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="63b9a-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="63b9a-244">Por ejemplo, en hello Shell de Mongo; para ello, ejecute operación Hola deseada tooverify Hola solicitud gratuito.</span><span class="sxs-lookup"><span data-stu-id="63b9a-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="63b9a-245">A continuación, ejecute el comando de hello *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="63b9a-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="63b9a-246">Con esto en mente, un método para calcular la cantidad de Hola de rendimiento reservados requerido por la aplicación es cargo por unidad toorecord Hola solicitud asociado con la ejecución de las operaciones típicas con un elemento representativo utilizado por la aplicación y, a continuación, calcular el número de Hola de operaciones es posible anticipar realizar cada segundo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="63b9a-247">Si tiene tipos de elemento que variarán considerablemente en cuanto al número de hello y tamaño de las propiedades indizadas, a continuación, registre el cargo por unidad Hola operación aplicable solicitud asociada a cada uno *tipo* de elemento típico.</span><span class="sxs-lookup"><span data-stu-id="63b9a-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="63b9a-248">Uso de las métricas del Portal de la API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="63b9a-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="63b9a-249">Hola tooget de manera más sencilla cargos por una buena estimación de la unidad de solicitud de la API de base de datos de MongoDB es hello toouse [portal de Azure](https://portal.azure.com) métricas.</span><span class="sxs-lookup"><span data-stu-id="63b9a-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="63b9a-250">Con hello *número de solicitudes* y *cargo de solicitud* gráficos, puede obtener una estimación de cuántas unidades de solicitud cada operación es el número de unidades de solicitud y utilizar consumen tooone relativa otro.</span><span class="sxs-lookup"><span data-stu-id="63b9a-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![Métricas del Portal de la API de MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="63b9a-252">Un ejemplo de estimación de la unidad de solicitud</span><span class="sxs-lookup"><span data-stu-id="63b9a-252">A request unit estimation example</span></span>
<span data-ttu-id="63b9a-253">Considere la posibilidad de hello siguiente documento ~ 1KB:</span><span class="sxs-lookup"><span data-stu-id="63b9a-253">Consider hello following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="63b9a-254">Documentos se reduce en la base de datos de Azure Cosmos, por lo que el sistema Hola calcula el tamaño del documento de hello anterior es un poco menos de 1KB.</span><span class="sxs-lookup"><span data-stu-id="63b9a-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="63b9a-255">Hello tabla siguiente muestran solicitud aproximado cargos de unidad para las operaciones típicas de este elemento (cargo de unidad de solicitud aproximado Hola se da por supuesto que el nivel de coherencia de cuenta de hello está establecido demasiado "Sesión" y que todos los elementos se indizan automáticamente):</span><span class="sxs-lookup"><span data-stu-id="63b9a-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="63b9a-256">Operación</span><span class="sxs-lookup"><span data-stu-id="63b9a-256">Operation</span></span> | <span data-ttu-id="63b9a-257">Cargo de la unidad de solicitud</span><span class="sxs-lookup"><span data-stu-id="63b9a-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="63b9a-258">Crear elemento</span><span class="sxs-lookup"><span data-stu-id="63b9a-258">Create item</span></span> |<span data-ttu-id="63b9a-259">~15 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-259">~15 RU</span></span> |
| <span data-ttu-id="63b9a-260">Lectura de elemento</span><span class="sxs-lookup"><span data-stu-id="63b9a-260">Read item</span></span> |<span data-ttu-id="63b9a-261">~1 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-261">~1 RU</span></span> |
| <span data-ttu-id="63b9a-262">Consulta de elemento por identificador</span><span class="sxs-lookup"><span data-stu-id="63b9a-262">Query item by id</span></span> |<span data-ttu-id="63b9a-263">~2,5 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-263">~2.5 RU</span></span> |

<span data-ttu-id="63b9a-264">Además, esta tabla muestra solicitud aproximado cargos de unidad para las consultas habituales que se usan en la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="63b9a-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="63b9a-265">Consultar</span><span class="sxs-lookup"><span data-stu-id="63b9a-265">Query</span></span> | <span data-ttu-id="63b9a-266">Cargo de la unidad de solicitud</span><span class="sxs-lookup"><span data-stu-id="63b9a-266">Request Unit Charge</span></span> | <span data-ttu-id="63b9a-267">Número de elementos devueltos</span><span class="sxs-lookup"><span data-stu-id="63b9a-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="63b9a-268">Selección de alimentos por Id.</span><span class="sxs-lookup"><span data-stu-id="63b9a-268">Select food by id</span></span> |<span data-ttu-id="63b9a-269">~2,5 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-269">~2.5 RU</span></span> |<span data-ttu-id="63b9a-270">1</span><span class="sxs-lookup"><span data-stu-id="63b9a-270">1</span></span> |
| <span data-ttu-id="63b9a-271">Selección de alimentos por fabricante</span><span class="sxs-lookup"><span data-stu-id="63b9a-271">Select foods by manufacturer</span></span> |<span data-ttu-id="63b9a-272">~7 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-272">~7 RU</span></span> |<span data-ttu-id="63b9a-273">7</span><span class="sxs-lookup"><span data-stu-id="63b9a-273">7</span></span> |
| <span data-ttu-id="63b9a-274">Selección por grupo de alimentos y clasificación por peso</span><span class="sxs-lookup"><span data-stu-id="63b9a-274">Select by food group and order by weight</span></span> |<span data-ttu-id="63b9a-275">~70 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-275">~70 RU</span></span> |<span data-ttu-id="63b9a-276">100</span><span class="sxs-lookup"><span data-stu-id="63b9a-276">100</span></span> |
| <span data-ttu-id="63b9a-277">Selección de los 10 alimentos más importantes en un grupo de alimentos</span><span class="sxs-lookup"><span data-stu-id="63b9a-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="63b9a-278">~10 RU</span><span class="sxs-lookup"><span data-stu-id="63b9a-278">~10 RU</span></span> |<span data-ttu-id="63b9a-279">10</span><span class="sxs-lookup"><span data-stu-id="63b9a-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="63b9a-280">Cargos RU varían en función de número de Hola de elementos devueltos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="63b9a-281">Con esta información, se pueden estimar los requisitos de RU de Hola para este número de Hola de aplicación dado de operaciones y las consultas que se espera por segundo:</span><span class="sxs-lookup"><span data-stu-id="63b9a-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="63b9a-282">Operación o consulta</span><span class="sxs-lookup"><span data-stu-id="63b9a-282">Operation/Query</span></span> | <span data-ttu-id="63b9a-283">Número estimado por segundo</span><span class="sxs-lookup"><span data-stu-id="63b9a-283">Estimated number per second</span></span> | <span data-ttu-id="63b9a-284">RU necesarias</span><span class="sxs-lookup"><span data-stu-id="63b9a-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="63b9a-285">Crear elemento</span><span class="sxs-lookup"><span data-stu-id="63b9a-285">Create item</span></span> |<span data-ttu-id="63b9a-286">10</span><span class="sxs-lookup"><span data-stu-id="63b9a-286">10</span></span> |<span data-ttu-id="63b9a-287">150</span><span class="sxs-lookup"><span data-stu-id="63b9a-287">150</span></span> |
| <span data-ttu-id="63b9a-288">Lectura de elemento</span><span class="sxs-lookup"><span data-stu-id="63b9a-288">Read item</span></span> |<span data-ttu-id="63b9a-289">100</span><span class="sxs-lookup"><span data-stu-id="63b9a-289">100</span></span> |<span data-ttu-id="63b9a-290">100</span><span class="sxs-lookup"><span data-stu-id="63b9a-290">100</span></span> |
| <span data-ttu-id="63b9a-291">Selección de alimentos por fabricante</span><span class="sxs-lookup"><span data-stu-id="63b9a-291">Select foods by manufacturer</span></span> |<span data-ttu-id="63b9a-292">25</span><span class="sxs-lookup"><span data-stu-id="63b9a-292">25</span></span> |<span data-ttu-id="63b9a-293">175</span><span class="sxs-lookup"><span data-stu-id="63b9a-293">175</span></span> |
| <span data-ttu-id="63b9a-294">Selección por grupo de alimentos</span><span class="sxs-lookup"><span data-stu-id="63b9a-294">Select by food group</span></span> |<span data-ttu-id="63b9a-295">10</span><span class="sxs-lookup"><span data-stu-id="63b9a-295">10</span></span> |<span data-ttu-id="63b9a-296">700</span><span class="sxs-lookup"><span data-stu-id="63b9a-296">700</span></span> |
| <span data-ttu-id="63b9a-297">Selección de los 10 principales</span><span class="sxs-lookup"><span data-stu-id="63b9a-297">Select top 10</span></span> |<span data-ttu-id="63b9a-298">15</span><span class="sxs-lookup"><span data-stu-id="63b9a-298">15</span></span> |<span data-ttu-id="63b9a-299">150 en total</span><span class="sxs-lookup"><span data-stu-id="63b9a-299">150 Total</span></span> |

<span data-ttu-id="63b9a-300">En este caso, se espera un requisito de rendimiento medio de 1,275 RU/s.</span><span class="sxs-lookup"><span data-stu-id="63b9a-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="63b9a-301">Redondea hacia arriba toohello más cercano de 100, puede proporcionar 1.300 RU/s para la recopilación de esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="63b9a-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="63b9a-302"><a id="RequestRateTooLarge"></a> Superación de los límites de rendimiento reservados en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="63b9a-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="63b9a-303">Recuerde que el consumo de unidad de solicitud se evalúa como una tasa por segundo si presupuesto Hola está vacía.</span><span class="sxs-lookup"><span data-stu-id="63b9a-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="63b9a-304">Para las aplicaciones que superan Hola tasa de solicitud de aprovisionamiento de unidad para un contenedor, solicita toothat colección se limitarán hasta que la velocidad de hello cae por debajo del nivel de hello reservado.</span><span class="sxs-lookup"><span data-stu-id="63b9a-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="63b9a-305">Cuando se produce una limitación, servidor hello forma preferente finalizará solicitud Hola con RequestRateTooLargeException (código de estado HTTP 429) y Hola devuelto x reintento ms después de ms de encabezado, indicando Hola período de tiempo, en milisegundos, que Hola usuario debe esperar antes de solicitud de hello intentando de nuevo.</span><span class="sxs-lookup"><span data-stu-id="63b9a-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="63b9a-306">Si usas las consultas LINQ y SDK de cliente de .NET de hello y, a continuación, la mayoría de los casos de hello nunca tienen toodeal a esta excepción, como la versión actual de Hola de hello SDK del cliente .NET implícitamente detecta esta respuesta, aspectos Hola especificado por el servidor encabezado retry-after, y solicitud de Hola de reintentos.</span><span class="sxs-lookup"><span data-stu-id="63b9a-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="63b9a-307">A menos que su cuenta está obteniendo acceso al mismo tiempo varios clientes, el siguiente reintento de Hola se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="63b9a-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="63b9a-308">Si tiene más de un cliente de manera acumulativa funcionando por encima de la tasa de solicitud de hello, hello comportamiento para reintentar la predeterminada puede no ser suficiente y cliente de hello producirá un DocumentClientException con 429 toohello aplicación de código de estado.</span><span class="sxs-lookup"><span data-stu-id="63b9a-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="63b9a-309">En casos como éste, puede controlar el comportamiento de reintento y la lógica de error de la aplicación rutinas de control o un aumento de rendimiento reservados de hello para el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="63b9a-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="63b9a-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Superación de los límites de rendimiento reservados en la API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="63b9a-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="63b9a-311">Las aplicaciones que superan las unidades de solicitud de hello aprovisionado para una colección se limitarán hasta que la velocidad de hello cae por debajo del nivel de hello reservado.</span><span class="sxs-lookup"><span data-stu-id="63b9a-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="63b9a-312">Cuando se produce una limitación, Hola back-end forma preferente finalizará solicitud Hola con un *16500* código de error - *demasiado muchas solicitudes*.</span><span class="sxs-lookup"><span data-stu-id="63b9a-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="63b9a-313">De forma predeterminada, la API de MongoDB volverá a intentar automáticamente too10 horas antes de devolver un *demasiado muchas solicitudes* código de error.</span><span class="sxs-lookup"><span data-stu-id="63b9a-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="63b9a-314">Si recibe muchos *demasiado muchas solicitudes* códigos de error, debe pensar en cualquier comportamiento para reintentar la adición de rutinas de control de errores de la aplicación o [aumenta el rendimiento reservado de hello para la recopilación de hello](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="63b9a-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63b9a-315">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63b9a-315">Next steps</span></span>
<span data-ttu-id="63b9a-316">toolearn más información acerca de rendimiento reservados con bases de datos de la base de datos de Azure Cosmos, explorar estos recursos:</span><span class="sxs-lookup"><span data-stu-id="63b9a-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="63b9a-317">Precios de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="63b9a-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="63b9a-318">Creación de particiones en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="63b9a-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="63b9a-319">toolearn más información acerca de la base de datos de Cosmos de Azure, vea Hola base de datos de Azure Cosmos [documentación](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="63b9a-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="63b9a-320">tooget a trabajar con la escalabilidad y rendimiento de pruebas con la base de datos de Cosmos de Azure, consulte [pruebas de rendimiento y escala con base de datos de Azure Cosmos](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="63b9a-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
