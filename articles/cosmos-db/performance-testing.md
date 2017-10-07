---
title: aaaAzure Cosmos DB escala y pruebas de rendimiento | Documentos de Microsoft
description: "Obtenga información acerca de cómo escalar tooperform y pruebas de rendimiento con base de datos de Azure Cosmos"
keywords: pruebas de rendimiento
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="c568f-104">Pruebas de escala y rendimiento con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c568f-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="c568f-105">Las pruebas de escala y rendimiento representan un paso clave en el desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c568f-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="c568f-106">Para muchas aplicaciones, el nivel de base de datos de hello tiene un impacto significativo en Hola el rendimiento general y la escalabilidad, y es, por tanto, un componente esencial del rendimiento de las pruebas.</span><span class="sxs-lookup"><span data-stu-id="c568f-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="c568f-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) está diseñado específicamente para el escalado flexible y un rendimiento predecible y, por lo tanto, supone una elección excelente para aplicaciones que necesitan un nivel de base de datos de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c568f-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="c568f-108">Este artículo es una referencia para los desarrolladores que implementan conjuntos de pruebas de rendimiento para sus cargas de trabajo de Cosmos DB o evalúan Cosmos DB para escenarios de aplicaciones de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c568f-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="c568f-109">Se centra principalmente en las pruebas de rendimiento aislado de base de datos de hello, pero también incluye prácticas recomendadas para las aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="c568f-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="c568f-110">Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="c568f-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="c568f-111">¿Dónde puedo encontrar una aplicación cliente de .NET de ejemplo para pruebas de rendimiento de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c568f-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="c568f-112">¿Cómo se pueden alcanzar niveles de alto rendimiento con Cosmos DB desde mi aplicación cliente?</span><span class="sxs-lookup"><span data-stu-id="c568f-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="c568f-113">tooget a trabajar con código, descargue proyecto Hola de [ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="c568f-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="c568f-114">objetivo de Hola de esta aplicación es toodemonstrate prácticas recomendadas para extraer un mejor rendimiento de la base de datos de Cosmos con un número reducido de equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="c568f-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="c568f-115">Esto no realizó la capacidad de toodemonstrate Hola máxima del servicio de hello, que puede escalar limitlessly.</span><span class="sxs-lookup"><span data-stu-id="c568f-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="c568f-116">Si está buscando tooimprove de opciones de configuración de cliente DB Cosmos rendimiento, consulte [sugerencias de rendimiento de base de datos de Azure Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="c568f-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="c568f-117">Ejecutar la aplicación de prueba de rendimiento de Hola</span><span class="sxs-lookup"><span data-stu-id="c568f-117">Run hello performance testing application</span></span>
<span data-ttu-id="c568f-118">Hola tooget de manera más rápida iniciado es toocompile y ejemplo de Hola ejecución .NET a continuación, como se describe en estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="c568f-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="c568f-119">También puede revisar el código fuente de hello e implementar aplicaciones de cliente propio de tooyour configuraciones similares.</span><span class="sxs-lookup"><span data-stu-id="c568f-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="c568f-120">**Paso 1:** proyecto Hola de descarga de [ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), o en el repositorio de GitHub de Hola de bifurcación.</span><span class="sxs-lookup"><span data-stu-id="c568f-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="c568f-121">**Paso 2:** modificar la configuración de Hola de EndpointUrl, AuthorizationKey, CollectionThroughput y DocumentTemplate (opcional) en un archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="c568f-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="c568f-122">Antes de aprovisionar colecciones con un alto rendimiento, consulte toohello [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/) los costos de hello tooestimate por colección.</span><span class="sxs-lookup"><span data-stu-id="c568f-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="c568f-123">Base de datos de Azure Cosmos facturas almacenamiento y rendimiento de forma independiente en concreto cada hora, por lo que puede ahorrar costos al eliminar o reducir el rendimiento de las colecciones de base de datos de Azure Cosmos Hola después de realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="c568f-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="c568f-124">**Paso 3:** compilar y ejecutar la aplicación de consola de hello desde línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c568f-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="c568f-125">Obtendrá unos resultados similares a Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c568f-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="c568f-126">**Paso 4 (si es necesario):** Hola rendimiento notificado (RU/s) de la herramienta de hello debe ser Hola igual o mayor que el rendimiento aprovisionado Hola de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="c568f-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="c568f-127">De lo contrario, creciente hello DegreeOfParallelism en incrementos pequeños puede ayudarle a alcanzar el límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="c568f-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="c568f-128">Si meseta de rendimiento de Hola desde la aplicación cliente, iniciar varias instancias de la aplicación hello en Hola iguales o distintos equipos le ayudará a alcanzar el límite de hello aprovisionado en hello instancias diferentes.</span><span class="sxs-lookup"><span data-stu-id="c568f-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="c568f-129">Si necesita ayuda con este paso, escriba un correo electrónico tooaskcosmosdb@microsoft.com o presentar una incidencia de soporte técnico de hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c568f-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c568f-130">Una vez que tenga la aplicación hello ejecutando, puede probar diferentes [directivas de indexación](indexing-policies.md) y [niveles de coherencia](consistency-levels.md) toounderstand su impacto sobre el rendimiento y la latencia.</span><span class="sxs-lookup"><span data-stu-id="c568f-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="c568f-131">También puede revisar el código fuente de hello e implementar las aplicaciones de producción o de conjuntos de pruebas propias de tooyour de configuraciones similares.</span><span class="sxs-lookup"><span data-stu-id="c568f-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c568f-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c568f-132">Next steps</span></span>
<span data-ttu-id="c568f-133">En este artículo, vimos cómo puede realizar pruebas de rendimiento y escala con Cosmos DB usando una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="c568f-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="c568f-134">Consulte toohello vínculos siguientes para obtener información adicional sobre cómo trabajar con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c568f-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="c568f-135">Ejemplo de pruebas de rendimiento de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c568f-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="c568f-136">Tooimprove de opciones de configuración de cliente rendimiento de base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="c568f-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="c568f-137">Creación de particiones en el servidor en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c568f-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


