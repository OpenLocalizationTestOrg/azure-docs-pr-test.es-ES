---
title: 'Azure Cosmos DB: unidades de solicitud por minuto (RU/m) | Microsoft Docs'
description: "Obtenga información sobre cómo reducir el costo mediante el uso de unidades de solicitud por minuto."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="d20f6-103">Unidades de solicitud por minuto en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d20f6-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="d20f6-104">Azure Cosmos DB se ha diseñado para ayudarle a lograr un rendimiento rápido y predecible. Además, permite escalar sin problemas a medida que la aplicación crece.</span><span class="sxs-lookup"><span data-stu-id="d20f6-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="d20f6-105">Puede aprovisionar el rendimiento de un contenedor de Cosmos DB en granularidades de unidades de solicitud por segundo y por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="d20f6-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="d20f6-106">El procesamiento aprovisionado en granularidad por minuto se usa para administrar picos inesperados de la carga de trabajo producidos en una granularidad por segundo.</span><span class="sxs-lookup"><span data-stu-id="d20f6-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="d20f6-107">En este artículo se proporciona información general sobre el funcionamiento del aprovisionamiento de unidad de solicitud por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="d20f6-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="d20f6-108">Con el aprovisionamiento de RU/m, se pretende proporcionar un rendimiento predecible en torno a necesidades impredecibles (especialmente si tiene que ejecutar análisis en la parte superior de los datos operativos) y cargas de trabajo con picos.</span><span class="sxs-lookup"><span data-stu-id="d20f6-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="d20f6-109">Queremos que nuestros clientes consuman más el rendimiento que aprovisionan, de modo que puedan escalar con mayor rapidez y tranquilidad.</span><span class="sxs-lookup"><span data-stu-id="d20f6-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="d20f6-110">Después de leer este artículo, podrá responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="d20f6-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="d20f6-111">¿Cómo funciona una unidad de solicitud por minuto?</span><span class="sxs-lookup"><span data-stu-id="d20f6-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="d20f6-112">¿Qué diferencia existe entre unidad de solicitud por minuto y unidad de solicitud por segundo?</span><span class="sxs-lookup"><span data-stu-id="d20f6-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="d20f6-113">¿Cómo aprovisionar RU/m?</span><span class="sxs-lookup"><span data-stu-id="d20f6-113">How to provision RU/m?</span></span>
* <span data-ttu-id="d20f6-114">¿En qué escenario consideraré la posibilidad de aprovisionar la unidad de solicitud por minuto?</span><span class="sxs-lookup"><span data-stu-id="d20f6-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="d20f6-115">¿Cómo usar las métricas del portal para optimizar el costo y el rendimiento?</span><span class="sxs-lookup"><span data-stu-id="d20f6-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="d20f6-116">Defina qué tipo de solicitud puede consumir el presupuesto de RU/m.</span><span class="sxs-lookup"><span data-stu-id="d20f6-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="d20f6-117">Aprovisionamiento de unidades de solicitud por minuto (RU/m)</span><span class="sxs-lookup"><span data-stu-id="d20f6-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="d20f6-118">Al aprovisionar Azure Cosmos DB en la granularidad de unidad de solicitud por segundo (RU/s), cuenta con la garantía de que su solicitud se realizará correctamente con baja latencia si el rendimiento no ha superado la capacidad aprovisionada durante ese segundo.</span><span class="sxs-lookup"><span data-stu-id="d20f6-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="d20f6-119">Con RU/m, la granularidad ofrece de forma inmediata la garantía de que su solicitud se realizará correctamente durante ese minuto.</span><span class="sxs-lookup"><span data-stu-id="d20f6-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="d20f6-120">En comparación con los sistemas de ampliación, nos aseguramos de que el rendimiento que obtiene sea predecible y pueda planearlo.</span><span class="sxs-lookup"><span data-stu-id="d20f6-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="d20f6-121">El funcionamiento del aprovisionamiento por minuto es sencillo:</span><span class="sxs-lookup"><span data-stu-id="d20f6-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="d20f6-122">RU/m se factura cada hora y aparte de RU/s.</span><span class="sxs-lookup"><span data-stu-id="d20f6-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="d20f6-123">Para obtener más información, visite la [página de precios](https://aka.ms/acdbpricing) de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d20f6-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="d20f6-124">RU/m se puede habilitar en el nivel de colección.</span><span class="sxs-lookup"><span data-stu-id="d20f6-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="d20f6-125">Esto es posible a través de los SDK (Node.js, Java o .NET) o del portal (también se incluyen las cargas de trabajo de API de MongoDB)</span><span class="sxs-lookup"><span data-stu-id="d20f6-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="d20f6-126">Al habilitarse RU/m, por cada 100 RU/s aprovisionadas, también obtiene 1000 RU/m aprovisionadas (la proporción es 10 veces mayor)</span><span class="sxs-lookup"><span data-stu-id="d20f6-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="d20f6-127">En un segundo determinado, una unidad de solicitud consume su aprovisionamiento de RU/m solo si ha superado su aprovisionamiento por segundo durante ese segundo</span><span class="sxs-lookup"><span data-stu-id="d20f6-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="d20f6-128">Una vez finalizado el período de 60 segundos (UTC), el aprovisionamiento por minuto se ha rellenado</span><span class="sxs-lookup"><span data-stu-id="d20f6-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="d20f6-129">RU/m se puede habilitar solo para colecciones con un aprovisionamiento máximo de 5000 RU/s por partición.</span><span class="sxs-lookup"><span data-stu-id="d20f6-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="d20f6-130">Si escala sus necesidades de rendimiento y tiene ese alto nivel de aprovisionamiento por partición, recibirá un mensaje de advertencia</span><span class="sxs-lookup"><span data-stu-id="d20f6-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="d20f6-131">A continuación vemos un ejemplo concreto, en el cual un cliente puede aprovisionar 10 000 RU/s con 100 000 RU/m, ahorrando un 73 % del costo frente al aprovisionamiento por pico (en 50 000 RU/seg.) a través de un período de 90 segundos de una colección que tiene 10 000 RU/s y 100 000 RU/m aprovisionados:</span><span class="sxs-lookup"><span data-stu-id="d20f6-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="d20f6-132">Primer segundo: el presupuesto de RU/m se establece en 100 000</span><span class="sxs-lookup"><span data-stu-id="d20f6-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="d20f6-133">Tercer segundo: durante ese segundo, el consumo de la unidad de solicitud era de 11 010 RU, 1010 RU por encima del aprovisionamiento de RU/s.</span><span class="sxs-lookup"><span data-stu-id="d20f6-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="d20f6-134">Por consiguiente, se deducen 1010 RU del presupuesto de RU/m.</span><span class="sxs-lookup"><span data-stu-id="d20f6-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="d20f6-135">98 990 RU están disponibles durante los próximos 57 segundos en el presupuesto de RU/m</span><span class="sxs-lookup"><span data-stu-id="d20f6-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="d20f6-136">Vigésimo noveno segundo: durante ese segundo, tuvo lugar un pico grande (más de cuatro veces superior al aprovisionamiento por segundo), mientras que el consumo de la unidad de solicitud era de 46 920 RU.</span><span class="sxs-lookup"><span data-stu-id="d20f6-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="d20f6-137">Se deducen 36 920 RU del presupuesto de RU/m que cayó de 92 323 RU (vigésimo octavo segundo) a 55 403 RU (vigésimo noveno segundo)</span><span class="sxs-lookup"><span data-stu-id="d20f6-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="d20f6-138">Sexagésimo primer segundo: el presupuesto de RU/m se establece de nuevo en 100 000 RU.</span><span class="sxs-lookup"><span data-stu-id="d20f6-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![Gráfico donde se muestra el consumo y el aprovisionamiento de Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="d20f6-140">Especificación de la capacidad de unidad de solicitud con RU/m</span><span class="sxs-lookup"><span data-stu-id="d20f6-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="d20f6-141">Al crear una colección de Azure Cosmos DB, especifique el número de unidades de solicitud por segundo (RU por segundo) que desee reservar para la colección.</span><span class="sxs-lookup"><span data-stu-id="d20f6-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="d20f6-142">También puede decidir si desea agregar RU por minuto.</span><span class="sxs-lookup"><span data-stu-id="d20f6-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="d20f6-143">Esto se puede hacer a través del portal o el SDK.</span><span class="sxs-lookup"><span data-stu-id="d20f6-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="d20f6-144">A través del portal</span><span class="sxs-lookup"><span data-stu-id="d20f6-144">Through the Portal</span></span>

<span data-ttu-id="d20f6-145">Para habilitar o deshabilitar RU por minuto, basta con hacer un solo clic al aprovisionar una colección.</span><span class="sxs-lookup"><span data-stu-id="d20f6-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Captura de pantalla donde se muestra cómo establecer RU/m en Azure Portal](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="d20f6-147">A través del SDK</span><span class="sxs-lookup"><span data-stu-id="d20f6-147">Through the SDK</span></span>
<span data-ttu-id="d20f6-148">En primer lugar, es importante tener en cuenta que RU/m solo está disponible para los siguientes SDK:</span><span class="sxs-lookup"><span data-stu-id="d20f6-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="d20f6-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="d20f6-149">.Net 1.14.0</span></span>
* <span data-ttu-id="d20f6-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d20f6-150">Java 1.11.0</span></span>
* <span data-ttu-id="d20f6-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d20f6-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="d20f6-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="d20f6-152">Python 2.2.0</span></span>

<span data-ttu-id="d20f6-153">Este es un fragmento de código para crear una colección con 3000 unidades de solicitud por segundo y 30 000 unidades de solicitud por minuto con el SDK de .NET:</span><span class="sxs-lookup"><span data-stu-id="d20f6-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="d20f6-154">A continuación se muestra un fragmento de código para cambiar el rendimiento de la colección a 5000 unidades de solicitud por segundo sin aprovisionar RU por minuto mediante el SDK de .NET:</span><span class="sxs-lookup"><span data-stu-id="d20f6-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="d20f6-155">Escenarios de buen ajuste</span><span class="sxs-lookup"><span data-stu-id="d20f6-155">Good fit scenarios</span></span>

<span data-ttu-id="d20f6-156">En esta sección, proporcionamos información general de escenarios de buen ajuste para habilitar unidades de solicitud por minuto.</span><span class="sxs-lookup"><span data-stu-id="d20f6-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="d20f6-157">**Entorno de desarrollo y pruebas:** buen ajuste.</span><span class="sxs-lookup"><span data-stu-id="d20f6-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="d20f6-158">Durante la fase de desarrollo, si prueba la aplicación con diversas cargas de trabajo, RU/m puede proporcionar la flexibilidad en esta fase.</span><span class="sxs-lookup"><span data-stu-id="d20f6-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="d20f6-159">El [emulador](local-emulator.md), por otra parte, es una herramienta gratuita excelente para probar Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d20f6-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="d20f6-160">Sin embargo, si desea empezar en un entorno en la nube, dispondrá de una gran flexibilidad con RU/m para sus necesidades de rendimiento ad hoc.</span><span class="sxs-lookup"><span data-stu-id="d20f6-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="d20f6-161">Pasará más tiempo desarrollando que preocupándose de las necesidades de rendimiento al principio.</span><span class="sxs-lookup"><span data-stu-id="d20f6-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="d20f6-162">Recomendamos empezar con el aprovisionamiento de RU/s mínimo y habilitar RU/m.</span><span class="sxs-lookup"><span data-stu-id="d20f6-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="d20f6-163">**Necesidades de granularidad de minuto con picos impredecibles:** buen ajuste. Ahorro: 25-75 %.</span><span class="sxs-lookup"><span data-stu-id="d20f6-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="d20f6-164">Hemos observado una gran mejora con respecto a RU/m, estando en dicho grupo la mayoría de los escenarios de producción.</span><span class="sxs-lookup"><span data-stu-id="d20f6-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="d20f6-165">Si tiene una carga de trabajo de IoT que se ha disparado varias veces en un minuto o consultas que se ejecutan cuando el sistema realiza inserción masiva al mismo tiempo, necesitará capacidad adicional para administrar las necesidades de los picos.</span><span class="sxs-lookup"><span data-stu-id="d20f6-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="d20f6-166">Recomendamos optimizar sus necesidades de recursos aplicando nuestro enfoque paso a paso a continuación.</span><span class="sxs-lookup"><span data-stu-id="d20f6-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Gráfico donde se muestra el consumo de la solicitud en una granularidad de cinco minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="d20f6-168">*Ilustración: prueba comparativa de consumo de RU*</span><span class="sxs-lookup"><span data-stu-id="d20f6-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="d20f6-169">**Tranquilidad:** buen ajuste. Ahorro: 10-20 %.</span><span class="sxs-lookup"><span data-stu-id="d20f6-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="d20f6-170">A veces, solo desea una mayor tranquilidad y no preocuparse tanto de los posibles picos, así como de la limitación.</span><span class="sxs-lookup"><span data-stu-id="d20f6-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="d20f6-171">Esta característica es la adecuada para usted.</span><span class="sxs-lookup"><span data-stu-id="d20f6-171">This feature is the right one for you.</span></span> <span data-ttu-id="d20f6-172">En ese caso, recomendamos habilitar RU/m y, de un modo ligeramente menos intenso, su aprovisionamiento por segundo.</span><span class="sxs-lookup"><span data-stu-id="d20f6-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="d20f6-173">Este caso es distinto del anterior, ya que usted no intentará optimizar su aprovisionamiento agresivamente.</span><span class="sxs-lookup"><span data-stu-id="d20f6-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="d20f6-174">Esto es más como una mentalidad de “limitación cero” que adopta.</span><span class="sxs-lookup"><span data-stu-id="d20f6-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="d20f6-175">Operaciones críticas con necesidades ad hoc: en ocasiones, recomendamos permitir únicamente a las operaciones críticas tener acceso al presupuesto de RU/m para que las operaciones ad hoc o menos importantes no lo consuman.</span><span class="sxs-lookup"><span data-stu-id="d20f6-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="d20f6-176">Esto puede definirse fácilmente en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="d20f6-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="d20f6-177">Uso de las métricas del portal para optimizar el costo y el rendimiento</span><span class="sxs-lookup"><span data-stu-id="d20f6-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="d20f6-178">**En las próximas semanas, desarrollaremos más el contenido en torno a la supervisión del consumo de minutos de RU para optimizar sus necesidades de rendimiento.**</span><span class="sxs-lookup"><span data-stu-id="d20f6-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="d20f6-179">A través de las métricas del portal, puede ver cuántos de los segundos de RU normales consume en comparación con los minutos de RU.</span><span class="sxs-lookup"><span data-stu-id="d20f6-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="d20f6-180">La supervisión de estas métricas debe ayudarle a optimizar su aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="d20f6-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="d20f6-181">Recomendamos un enfoque paso a paso sobre cómo usar RU/m para su beneficio.</span><span class="sxs-lookup"><span data-stu-id="d20f6-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="d20f6-182">En cada paso, debe disponer de información general del consumo de RU que representa un ciclo completo de su carga de trabajo (podrían ser horas, días o incluso semanas) y obtener información sobre el uso de aquello que aprovisiona.</span><span class="sxs-lookup"><span data-stu-id="d20f6-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="d20f6-183">El principio que subyace a este enfoque es hacer que su aprovisionamiento de rendimiento esté lo más cerca posible de un punto de aprovisionamiento que coincida con sus criterios de rendimiento mostrados a continuación.</span><span class="sxs-lookup"><span data-stu-id="d20f6-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![Gráfico donde se muestra el consumo de la solicitud en una granularidad de cinco minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="d20f6-185">Para entender el punto de aprovisionamiento óptimo de su carga de trabajo, debe entender lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d20f6-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="d20f6-186">Patrones de consumo: ¿picos inexistentes, poco frecuentes o sostenidos?</span><span class="sxs-lookup"><span data-stu-id="d20f6-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="d20f6-187">¿Picos pequeños (doble de media), medios o grandes (más de 10 veces de media)?</span><span class="sxs-lookup"><span data-stu-id="d20f6-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="d20f6-188">Porcentaje de solicitudes limitadas: ¿se siente cómodo en caso de tener un poco de limitación?</span><span class="sxs-lookup"><span data-stu-id="d20f6-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="d20f6-189">Si es así, ¿en qué medida?</span><span class="sxs-lookup"><span data-stu-id="d20f6-189">If so, by how much?</span></span> 

<span data-ttu-id="d20f6-190">Una vez que haya identificado cuáles son sus objetivos, podrá estar más cerca del aprovisionamiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="d20f6-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="d20f6-191">Para ayudarle, queremos facilitar orientación general sobre cómo optimizar su aprovisionamiento en función de su consumo de RU/m.</span><span class="sxs-lookup"><span data-stu-id="d20f6-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="d20f6-192">Dicha orientación no se aplica a todos los tipos de cargas de trabajo, pero se basa en el conocimiento de la vista previa privada.</span><span class="sxs-lookup"><span data-stu-id="d20f6-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="d20f6-193">Puede que cambiemos estas líneas base a medida que obtenemos más información:</span><span class="sxs-lookup"><span data-stu-id="d20f6-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="d20f6-194">RU/m % uso</span><span class="sxs-lookup"><span data-stu-id="d20f6-194">RU/m % utilization</span></span>|<span data-ttu-id="d20f6-195">Grado de uso de RU/m</span><span class="sxs-lookup"><span data-stu-id="d20f6-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="d20f6-196">Medidas recomendadas para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="d20f6-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="d20f6-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="d20f6-197">0-1%</span></span>|<span data-ttu-id="d20f6-198">En uso</span><span class="sxs-lookup"><span data-stu-id="d20f6-198">Under utilization</span></span>|<span data-ttu-id="d20f6-199">Reducir RU/s para consumir más RU/m</span><span class="sxs-lookup"><span data-stu-id="d20f6-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="d20f6-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="d20f6-200">1-10%</span></span>|<span data-ttu-id="d20f6-201">Uso correcto</span><span class="sxs-lookup"><span data-stu-id="d20f6-201">Healthy use</span></span>|<span data-ttu-id="d20f6-202">Mantener el mismo nivel de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="d20f6-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="d20f6-203">Por encima del 10%</span><span class="sxs-lookup"><span data-stu-id="d20f6-203">Above 10%</span></span>|<span data-ttu-id="d20f6-204">Uso excesivo</span><span class="sxs-lookup"><span data-stu-id="d20f6-204">Over utilization</span></span>|<span data-ttu-id="d20f6-205">Aumentar RU/s para depender en menor grado de RU/m</span><span class="sxs-lookup"><span data-stu-id="d20f6-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="d20f6-206">Selección de las operaciones que pueden consumir el presupuesto de RU/m</span><span class="sxs-lookup"><span data-stu-id="d20f6-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="d20f6-207">En el nivel de solicitud, también puede habilitar o deshabilitar el presupuesto de RU/m para atender la solicitud con independencia del tipo de operación. </span><span class="sxs-lookup"><span data-stu-id="d20f6-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="d20f6-208">Si se consume el presupuesto de RU/seg. aprovisionado normal y la solicitud no puede consumir el presupuesto de RU/m, esta solicitud se limitará.</span><span class="sxs-lookup"><span data-stu-id="d20f6-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="d20f6-209">De forma predeterminada, el presupuesto de RU/m atiende todas las solicitudes si se activa el presupuesto de rendimiento de RU/m.</span><span class="sxs-lookup"><span data-stu-id="d20f6-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="d20f6-210">A continuación se muestra un fragmento de código para deshabilitar el presupuesto de RU/m mediante la API de DocumentDB para operaciones de CRUD y de consulta.</span><span class="sxs-lookup"><span data-stu-id="d20f6-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="d20f6-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d20f6-211">Next steps</span></span>

<span data-ttu-id="d20f6-212">En este artículo hemos descrito el funcionamiento de las particiones en Azure Cosmos DB, cómo crear colecciones particionadas y cómo elegir una buena clave de partición para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d20f6-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="d20f6-213">Realice pruebas de escala y de rendimiento con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d20f6-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="d20f6-214">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md) para ver ejemplos.</span><span class="sxs-lookup"><span data-stu-id="d20f6-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="d20f6-215">Introducción a la codificación con los [SDK](documentdb-sdk-dotnet.md) o la [API de REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d20f6-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="d20f6-216">Información sobre el [procesamiento aprovisionado](request-units.md) en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d20f6-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

