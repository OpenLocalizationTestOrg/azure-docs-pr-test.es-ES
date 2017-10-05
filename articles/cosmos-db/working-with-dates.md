---
title: Trabajo con fechas en Azure Cosmos DB | Microsoft Docs
description: Aprenda a trabajar con fechas en Azure Cosmos DB.
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: b6a77e33eea24000037ffb31d7aae3cb1d345ce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="43626-103">Trabajo con fechas en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="43626-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="43626-104">Azure Cosmos DB proporciona flexibilidad de esquema e indexación completa mediante un modelo de datos [JSON](http://www.json.org) nativo.</span><span class="sxs-lookup"><span data-stu-id="43626-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="43626-105">Todos los recursos de Azure Cosmos DB, incluidas las bases de datos, las colecciones, los documentos y los procedimientos almacenados están modelados y almacenados como documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="43626-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="43626-106">Como requisito para ser portátil, JSON (y Azure Cosmos DB) solo admite un pequeño conjunto de tipos básicos: cadena, número, booleano, matriz, objeto y null.</span><span class="sxs-lookup"><span data-stu-id="43626-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="43626-107">Sin embargo, JSON es flexible y permite que los desarrolladores y marcos de trabajo representen tipos más complejos mediante estos primitivos y los compongan como objetos o matrices.</span><span class="sxs-lookup"><span data-stu-id="43626-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="43626-108">Además de los tipos básicos, muchas aplicaciones necesitan el tipo [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) para representar fechas y marcas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="43626-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="43626-109">En este artículo se explica cómo los desarrolladores pueden almacenar, recuperar y consultar fechas en Azure Cosmos DB mediante el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="43626-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="43626-110">Almacenamiento de valores DateTime</span><span class="sxs-lookup"><span data-stu-id="43626-110">Storing DateTimes</span></span>
<span data-ttu-id="43626-111">De forma predeterminada, el [SDK de Azure Cosmos DB](documentdb-sdk-dotnet.md) serializa los valores DateTime como cadenas [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874).</span><span class="sxs-lookup"><span data-stu-id="43626-111">By default, the [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="43626-112">La mayoría de las aplicaciones pueden la representación de cadena predeterminada para DateTime por los siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="43626-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="43626-113">Las cadenas se pueden comparar, y se conserva el orden relativo de los valores DateTime cuando se transforman en cadenas.</span><span class="sxs-lookup"><span data-stu-id="43626-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="43626-114">Este enfoque no requiere ninguna personalización del código o de los atributos para la conversión de JSON.</span><span class="sxs-lookup"><span data-stu-id="43626-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="43626-115">Las fechas almacenadas en JSON son legibles para el usuario.</span><span class="sxs-lookup"><span data-stu-id="43626-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="43626-116">Este enfoque puede aprovechar el índice de Azure Cosmos DB para aumentar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="43626-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="43626-117">Por ejemplo, el fragmento de código siguiente almacena un objeto `Order` que contiene dos propiedades de DateTime: `ShipDate` y `OrderDate` como un documento mediante el SDK de .NET:</span><span class="sxs-lookup"><span data-stu-id="43626-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="43626-118">Este documento se almacena en Azure Cosmos DB de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="43626-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="43626-119">Como alternativa, puede almacenar valores DateTime como marcas de tiempo de Unix, es decir, como un número que representa el número de segundos transcurridos desde el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="43626-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="43626-120">La propiedad Timestamp (`_ts`) interna de Azure Cosmos DB sigue este enfoque.</span><span class="sxs-lookup"><span data-stu-id="43626-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="43626-121">Puede usar la clase [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) clase para serializar los valores DateTime como números.</span><span class="sxs-lookup"><span data-stu-id="43626-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="43626-122">Indexación de valores DateTime para consultas de rango</span><span class="sxs-lookup"><span data-stu-id="43626-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="43626-123">Las consultas de rango son comunes con valores DateTime.</span><span class="sxs-lookup"><span data-stu-id="43626-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="43626-124">Por ejemplo, si necesita encontrar todos los pedidos que se crearon desde ayer o todos los pedidos enviados en los últimos cinco minutos, debe realizar las consultas de rango.</span><span class="sxs-lookup"><span data-stu-id="43626-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="43626-125">Para ejecutar estas consultas de forma eficaz, debe configurar la colección para la indización de rangos en cadenas.</span><span class="sxs-lookup"><span data-stu-id="43626-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="43626-126">Puede aprender más sobre cómo configurar directivas de indexación en [¿Cómo funcionan los datos del índice de Azure Cosmos DB?](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="43626-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="43626-127">Consulta de valores DateTimes en LINQ</span><span class="sxs-lookup"><span data-stu-id="43626-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="43626-128">El SDK de .NET para DocumentDB admite automáticamente la consulta de datos almacenados en Azure Cosmos DB mediante LINQ.</span><span class="sxs-lookup"><span data-stu-id="43626-128">The DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="43626-129">Por ejemplo, el fragmento de código siguiente muestra una consulta LINQ que ordena los filtros que se enviaron en los últimos tres días.</span><span class="sxs-lookup"><span data-stu-id="43626-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="43626-130">Puede aprender más sobre el lenguaje de consulta SQL de Azure Cosmos DB y el proveedor LINQ en [Consulta de Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="43626-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="43626-131">En este artículo se explica cómo almacenar, indexar y consultar valores DateTime en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="43626-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43626-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43626-132">Next Steps</span></span>
* <span data-ttu-id="43626-133">Descargue y ejecute los [ejemplos de código en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples).</span><span class="sxs-lookup"><span data-stu-id="43626-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="43626-134">Obtener más información en [Consulta de API de DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="43626-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="43626-135">Obtener más información sobre [Directivas de indexación de Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="43626-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
