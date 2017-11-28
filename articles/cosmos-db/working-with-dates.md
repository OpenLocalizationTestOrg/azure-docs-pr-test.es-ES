---
title: aaaWorking con fechas en la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toowork con las fechas en la base de datos de Azure Cosmos."
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
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="f39d3-103">Trabajo con fechas en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f39d3-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="f39d3-104">Azure Cosmos DB proporciona flexibilidad de esquema e indexación completa mediante un modelo de datos [JSON](http://www.json.org) nativo.</span><span class="sxs-lookup"><span data-stu-id="f39d3-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="f39d3-105">Todos los recursos de Azure Cosmos DB, incluidas las bases de datos, las colecciones, los documentos y los procedimientos almacenados están modelados y almacenados como documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="f39d3-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="f39d3-106">Como requisito para ser portátil, JSON (y Azure Cosmos DB) solo admite un pequeño conjunto de tipos básicos: cadena, número, booleano, matriz, objeto y null.</span><span class="sxs-lookup"><span data-stu-id="f39d3-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="f39d3-107">Sin embargo, JSON es flexible y permitir a los desarrolladores y marcos de trabajo toorepresent tipos más complejos con estas primitivas y creándolos a como objetos o matrices.</span><span class="sxs-lookup"><span data-stu-id="f39d3-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="f39d3-108">En tipos básicos de suma toohello, muchas aplicaciones necesitan hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) escriba toorepresent fechas y las marcas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="f39d3-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="f39d3-109">Este artículo describe cómo los desarrolladores pueden almacenar, recuperar y consultar las fechas en la base de datos de Azure Cosmos con hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="f39d3-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="f39d3-110">Almacenamiento de valores DateTime</span><span class="sxs-lookup"><span data-stu-id="f39d3-110">Storing DateTimes</span></span>
<span data-ttu-id="f39d3-111">De forma predeterminada, Hola [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) serializa los valores de fecha y hora como [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) cadenas.</span><span class="sxs-lookup"><span data-stu-id="f39d3-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="f39d3-112">Mayoría de las aplicaciones puede utilizar representación de cadena de saludo predeterminado de fecha y hora para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="f39d3-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="f39d3-113">Se pueden comparar cadenas y Hola relativa de ordenación de los valores de fecha y hora de Hola se conserva cuando están toostrings transformado.</span><span class="sxs-lookup"><span data-stu-id="f39d3-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="f39d3-114">Este enfoque no requiere ninguna personalización del código o de los atributos para la conversión de JSON.</span><span class="sxs-lookup"><span data-stu-id="f39d3-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="f39d3-115">las fechas de Hello tal como se almacena en JSON son humanas legible.</span><span class="sxs-lookup"><span data-stu-id="f39d3-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="f39d3-116">Este enfoque puede aprovechar el índice de Azure Cosmos DB para aumentar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="f39d3-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="f39d3-117">Por ejemplo, Hola siguientes almacenes de fragmento de código una `Order` objeto que contiene dos propiedades de fecha y hora - `ShipDate` y `OrderDate` como un documento utilizando Hola .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="f39d3-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

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

<span data-ttu-id="f39d3-118">Este documento se almacena en Azure Cosmos DB de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="f39d3-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="f39d3-119">Como alternativa, puede almacenar fechas y horas como las marcas de hora de Unix, es decir, como un número que representa el número de Hola de segundos transcurridos desde el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="f39d3-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="f39d3-120">La propiedad Timestamp (`_ts`) interna de Azure Cosmos DB sigue este enfoque.</span><span class="sxs-lookup"><span data-stu-id="f39d3-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="f39d3-121">Puede usar hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) clase tooserialize fechas y horas como números.</span><span class="sxs-lookup"><span data-stu-id="f39d3-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="f39d3-122">Indexación de valores DateTime para consultas de rango</span><span class="sxs-lookup"><span data-stu-id="f39d3-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="f39d3-123">Las consultas de rango son comunes con valores DateTime.</span><span class="sxs-lookup"><span data-stu-id="f39d3-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="f39d3-124">Por ejemplo, si necesita toofind todas las órdenes creadas desde ayer, o buscar todos los pedidos enviados en hello últimos cinco minutos, deberá tooperform consultas por rango.</span><span class="sxs-lookup"><span data-stu-id="f39d3-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="f39d3-125">tooexecute estas consultas de forma eficaz, debe configurar la colección para la indización de intervalo en cadenas.</span><span class="sxs-lookup"><span data-stu-id="f39d3-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="f39d3-126">Puede aprender más acerca de cómo tooconfigure directivas en la indización [directivas de indización de base de datos de Azure Cosmos](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f39d3-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="f39d3-127">Consulta de valores DateTimes en LINQ</span><span class="sxs-lookup"><span data-stu-id="f39d3-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="f39d3-128">Hola documentos .NET SDK automáticamente permite consultar los datos almacenados en la base de datos de Azure Cosmos mediante LINQ.</span><span class="sxs-lookup"><span data-stu-id="f39d3-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="f39d3-129">Por ejemplo, hello fragmento de código siguiente muestra una consulta LINQ que ordena los filtros que se enviaron en hello últimos tres días.</span><span class="sxs-lookup"><span data-stu-id="f39d3-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="f39d3-130">Puede aprender más acerca consulta hello y lenguaje LINQ proveedor de SQL de Azure Cosmos DB en [consultar Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="f39d3-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="f39d3-131">En este artículo, explicamos cómo toostore, indizar y consultar las fechas y horas en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f39d3-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f39d3-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f39d3-132">Next Steps</span></span>
* <span data-ttu-id="f39d3-133">Descargue y ejecute hello [ejemplos en GitHub de código](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="f39d3-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="f39d3-134">Obtener más información en [Consulta de API de DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="f39d3-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="f39d3-135">Obtener más información sobre [Directivas de indexación de Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="f39d3-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
