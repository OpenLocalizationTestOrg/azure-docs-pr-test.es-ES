---
title: Pruebas de escala y rendimiento de Azure Cosmos DB | Microsoft Docs
description: "Más información sobre cómo realizar pruebas de escala y de rendimiento con Azure Cosmos DB"
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
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="ac11c-104">Pruebas de escala y rendimiento con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ac11c-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="ac11c-105">Las pruebas de escala y rendimiento representan un paso clave en el desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ac11c-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="ac11c-106">Para muchas aplicaciones, el nivel de la base de datos repercute significativamente en la escalabilidad y el rendimiento generales y, por tanto, es un componente esencial de las pruebas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ac11c-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="ac11c-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) está diseñado específicamente para el escalado flexible y un rendimiento predecible y, por lo tanto, supone una elección excelente para aplicaciones que necesitan un nivel de base de datos de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ac11c-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="ac11c-108">Este artículo es una referencia para los desarrolladores que implementan conjuntos de pruebas de rendimiento para sus cargas de trabajo de Cosmos DB o evalúan Cosmos DB para escenarios de aplicaciones de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ac11c-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="ac11c-109">Se centra principalmente en las pruebas de rendimiento aislado de la base de datos, pero también incluye prácticas recomendadas para las aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="ac11c-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="ac11c-110">Después de leer este artículo, podrá responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="ac11c-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="ac11c-111">¿Dónde puedo encontrar una aplicación cliente de .NET de ejemplo para pruebas de rendimiento de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="ac11c-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="ac11c-112">¿Cómo se pueden alcanzar niveles de alto rendimiento con Cosmos DB desde mi aplicación cliente?</span><span class="sxs-lookup"><span data-stu-id="ac11c-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="ac11c-113">Para empezar a trabajar con código, descargue el proyecto del [ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="ac11c-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="ac11c-114">El objetivo de esta aplicación es demostrar las mejores prácticas para sacarle un mayor partido a Cosmos DB con un pequeño número de equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="ac11c-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="ac11c-115">La finalidad no es demostrar la capacidad máxima del servicio, que puede ampliarse sin límites.</span><span class="sxs-lookup"><span data-stu-id="ac11c-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="ac11c-116">Si busca opciones de configuración de cliente para mejorar el rendimiento de Cosmos DB, consulte [Sugerencias de rendimiento para Azure Cosmos DB](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="ac11c-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="ac11c-117">Ejecute la aplicación de pruebas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="ac11c-117">Run the performance testing application</span></span>
<span data-ttu-id="ac11c-118">La forma más rápida de empezar es compilar y ejecutar este ejemplo de .NET, tal como se describe en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="ac11c-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="ac11c-119">También puede revisar el código fuente e implementar configuraciones similares a sus propias aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="ac11c-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="ac11c-120">**Paso 1:** descargue el proyecto del [ejemplo de pruebas de rendimiento de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark) o bifurque el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="ac11c-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="ac11c-121">**Paso 2:** modifique la configuración de EndpointUrl, AuthorizationKey, CollectionThroughput y DocumentTemplate (opcional) en el archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="ac11c-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="ac11c-122">Antes de aprovisionar colecciones con un alto rendimiento, vea la [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/) para estimar los costos por colección.</span><span class="sxs-lookup"><span data-stu-id="ac11c-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="ac11c-123">Azure Cosmos DB factura el almacenamiento y el rendimiento de forma independiente por horas, por lo que puede ahorrar costos si elimina o reduce el rendimiento de las colecciones de Azure Cosmos DB una vez realizadas las pruebas.</span><span class="sxs-lookup"><span data-stu-id="ac11c-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="ac11c-124">**Paso 3:** compile y ejecute la aplicación de consola en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="ac11c-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="ac11c-125">El resultado debe ser parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac11c-125">You should see output like the following:</span></span>

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


<span data-ttu-id="ac11c-126">**Paso 4 (si es necesario):** el rendimiento notificado (RU/s) de la herramienta debe ser igual o mayor que el rendimiento de aprovisionamiento de la colección.</span><span class="sxs-lookup"><span data-stu-id="ac11c-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="ac11c-127">Si no es así, puede alcanzar el límite si aumenta el valor de DegreeOfParallelism en incrementos pequeños.</span><span class="sxs-lookup"><span data-stu-id="ac11c-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="ac11c-128">Si el rendimiento de la aplicación cliente se estanca, iniciar varias instancias de la aplicación en los mismos equipos u otros distintos lo ayudará a alcanzar el límite de aprovisionamiento en distintas instancias.</span><span class="sxs-lookup"><span data-stu-id="ac11c-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="ac11c-129">Si necesita ayuda con este paso, escriba un correo electrónico a askcosmosdb@microsoft.com o rellene una incidencia de soporte técnico desde [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac11c-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="ac11c-130">Una vez que se ejecute la aplicación, puede probar diferentes [directivas de indexación](indexing-policies.md) y [niveles de coherencia](consistency-levels.md) para conocer su repercusión en el rendimiento y la latencia.</span><span class="sxs-lookup"><span data-stu-id="ac11c-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="ac11c-131">También puede revisar el código fuente e implementar configuraciones similares a sus propios conjuntos de pruebas o aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="ac11c-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac11c-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac11c-132">Next steps</span></span>
<span data-ttu-id="ac11c-133">En este artículo, vimos cómo puede realizar pruebas de rendimiento y escala con Cosmos DB usando una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="ac11c-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="ac11c-134">Consulte los siguientes vínculos para obtener información adicional acerca de cómo trabajar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ac11c-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="ac11c-135">Ejemplo de pruebas de rendimiento de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ac11c-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="ac11c-136">Opciones de configuración de cliente para mejorar el rendimiento de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ac11c-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="ac11c-137">Creación de particiones en el servidor en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ac11c-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


