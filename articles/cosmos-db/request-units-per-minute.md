---
title: 'Azure Cosmos DB: unidades de solicitud por minuto (RU/m) | Microsoft Docs'
description: "Obtenga información acerca de cómo tooreduce costo, gracias a la solicitud de unidades por minuto."
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
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="052e5-103">Unidades de solicitud por minuto en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="052e5-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="052e5-104">Base de datos de Azure Cosmos es diseñada toohelp lograr un rendimiento rápido y predecible y escala perfectamente junto con el crecimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="052e5-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="052e5-105">Puede aprovisionar el rendimiento de un contenedor de Cosmos DB en granularidades de unidades de solicitud por segundo y por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="052e5-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="052e5-106">Hola rendimiento aprovisionado en una granularidad por minuto es toomanage usado inesperados picos de carga de trabajo de Hola que se producen en una granularidad por segundo.</span><span class="sxs-lookup"><span data-stu-id="052e5-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="052e5-107">Este artículo proporciona información general sobre cómo funciona el aprovisionamiento de saludo de solicitud unidad por minuto (RU/m).</span><span class="sxs-lookup"><span data-stu-id="052e5-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="052e5-108">objetivo de Hello en cuenta con el aprovisionamiento del RU/m es tooprovide un rendimiento predecible alrededor de las necesidades imprevisibles (especialmente si necesita toorun análisis sobre los datos operativos) y las cargas de trabajo picos.</span><span class="sxs-lookup"><span data-stu-id="052e5-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="052e5-109">Queremos toohave que nuestros clientes consumen más rendimiento Hola aprovisionan por lo que puede escalar rápidamente con la tranquilidad de saber.</span><span class="sxs-lookup"><span data-stu-id="052e5-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="052e5-110">Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="052e5-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="052e5-111">¿Cómo funciona una unidad de solicitud por minuto?</span><span class="sxs-lookup"><span data-stu-id="052e5-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="052e5-112">¿Cuál es la diferencia de hello entre solicitar unidad por minuto y unidad de solicitud por segundo?</span><span class="sxs-lookup"><span data-stu-id="052e5-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="052e5-113">¿Cómo tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="052e5-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="052e5-114">¿En qué escenario consideraré la posibilidad de aprovisionar la unidad de solicitud por minuto?</span><span class="sxs-lookup"><span data-stu-id="052e5-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="052e5-115">¿Cómo toouse Hola métricas portal toooptimize el costo y el rendimiento?</span><span class="sxs-lookup"><span data-stu-id="052e5-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="052e5-116">Defina qué tipo de solicitud puede consumir el presupuesto de RU/m.</span><span class="sxs-lookup"><span data-stu-id="052e5-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="052e5-117">Aprovisionamiento de unidades de solicitud por minuto (RU/m)</span><span class="sxs-lookup"><span data-stu-id="052e5-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="052e5-118">Al aprovisionar la base de datos de Azure Cosmos con granularidad de hello segundo (RU/s), obtendrá garantía de Hola que la solicitud es correcta en una latencia baja si el rendimiento no superó la capacidad de hello aprovisionado en ese segundo.</span><span class="sxs-lookup"><span data-stu-id="052e5-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="052e5-119">Con RU/m, la granularidad de Hola se encuentra en minuto Hola con garantía de Hola que la solicitud se realiza correctamente en ese minuto.</span><span class="sxs-lookup"><span data-stu-id="052e5-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="052e5-120">En comparación con los sistemas toobursting, nos aseguramos de que obtendrá de rendimiento de hello es predecible y piensa en ella.</span><span class="sxs-lookup"><span data-stu-id="052e5-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="052e5-121">Hola por minuto aprovisionamiento funciona de forma sencilla:</span><span class="sxs-lookup"><span data-stu-id="052e5-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="052e5-122">RU/m se factura cada hora y en suma tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="052e5-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="052e5-123">Para obtener más información, visite la [página de precios](https://aka.ms/acdbpricing) de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="052e5-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="052e5-124">RU/m se puede habilitar en el nivel de colección.</span><span class="sxs-lookup"><span data-stu-id="052e5-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="052e5-125">Esto puede realizarse a través de hello SDK (Node.js, Java o. NET) o a través del portal de hello (que también se incluyen las cargas de trabajo de la API de MongoDB)</span><span class="sxs-lookup"><span data-stu-id="052e5-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="052e5-126">Cuando se habilita RU/m, para cada 100 RU/s aprovisionado, también obtendrá 1.000 RU/m aprovisionado (relación de hello es x 10)</span><span class="sxs-lookup"><span data-stu-id="052e5-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="052e5-127">En un segundo determinado, una unidad de solicitud consume su aprovisionamiento de RU/m solo si ha superado su aprovisionamiento por segundo durante ese segundo</span><span class="sxs-lookup"><span data-stu-id="052e5-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="052e5-128">Una vez Hola finaliza el período de 60 segundos (UTC), se ha rellenado Hola por minuto de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="052e5-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="052e5-129">RU/m se puede habilitar solo para colecciones con un aprovisionamiento máximo de 5000 RU/s por partición.</span><span class="sxs-lookup"><span data-stu-id="052e5-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="052e5-130">Si escala sus necesidades de rendimiento y tiene ese alto nivel de aprovisionamiento por partición, recibirá un mensaje de advertencia</span><span class="sxs-lookup"><span data-stu-id="052e5-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="052e5-131">A continuación vemos un ejemplo concreto, en el cual un cliente puede aprovisionar 10 000 RU/s con 100 000 RU/m, ahorrando un 73 % del costo frente al aprovisionamiento por pico (en 50 000 RU/seg.) a través de un período de 90 segundos de una colección que tiene 10 000 RU/s y 100 000 RU/m aprovisionados:</span><span class="sxs-lookup"><span data-stu-id="052e5-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="052e5-132">1 segundo: asignación de hello RU/m se establece en 100 000</span><span class="sxs-lookup"><span data-stu-id="052e5-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="052e5-133">3er segundo: durante esa segunda aparición de Hola el consumo de unidad de la solicitud era 11,010 RUs, 1,010 RUs anteriormente Hola RU/s aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="052e5-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="052e5-134">Por lo tanto, 1,010 RUs se deducen del presupuesto RU/m de Hola.</span><span class="sxs-lookup"><span data-stu-id="052e5-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="052e5-135">Están disponibles para hello 98,990 RUs siguientes 57 segundos en presupuesto de hello RU/m</span><span class="sxs-lookup"><span data-stu-id="052e5-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="052e5-136">segundo 29: durante ese segundo, se produjo un pico grande (> 4 x superior aprovisionamiento por segundo) y el consumo de Hola de unidad de la solicitud era 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="052e5-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="052e5-137">36,920 RUs se deducen del presupuesto RU/m de Hola que quita de 92,323 too55 RUs (segundo 28), 403 RUs (29 segundos)</span><span class="sxs-lookup"><span data-stu-id="052e5-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="052e5-138">segundo 61st: presupuesto RU/m se vuelve a establecer too100, 000 RUs.</span><span class="sxs-lookup"><span data-stu-id="052e5-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Gráfico que muestra el consumo de Hola y el aprovisionamiento de la base de datos de Azure Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="052e5-140">Especificación de la capacidad de unidad de solicitud con RU/m</span><span class="sxs-lookup"><span data-stu-id="052e5-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="052e5-141">Al crear una colección de base de datos de Azure Cosmos, especifique el número de Hola de unidades de solicitud por segundo (RU por segundo) desea reservar para la recopilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="052e5-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="052e5-142">También puede decidir si desea tooadd RU por minuto.</span><span class="sxs-lookup"><span data-stu-id="052e5-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="052e5-143">Esto puede realizarse a través de hello Portal o hello SDK.</span><span class="sxs-lookup"><span data-stu-id="052e5-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="052e5-144">A través de hello Portal</span><span class="sxs-lookup"><span data-stu-id="052e5-144">Through hello Portal</span></span>

<span data-ttu-id="052e5-145">Para habilitar o deshabilitar RU por minuto, basta con hacer un solo clic al aprovisionar una colección.</span><span class="sxs-lookup"><span data-stu-id="052e5-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Captura de pantalla que se muestra cómo tooset RU/m Hola portal de Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="052e5-147">A través de hello SDK</span><span class="sxs-lookup"><span data-stu-id="052e5-147">Through hello SDK</span></span>
<span data-ttu-id="052e5-148">En primer lugar, se trata de toonote importante que RU/m solo está disponible para hello siguientes SDK:</span><span class="sxs-lookup"><span data-stu-id="052e5-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="052e5-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="052e5-149">.Net 1.14.0</span></span>
* <span data-ttu-id="052e5-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="052e5-150">Java 1.11.0</span></span>
* <span data-ttu-id="052e5-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="052e5-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="052e5-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="052e5-152">Python 2.2.0</span></span>

<span data-ttu-id="052e5-153">Este es un fragmento de código para crear una colección con 3.000 unidades de solicitud por unidades de solicitud de segundo y 30.000 por minuto con hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="052e5-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="052e5-154">Este es un fragmento de código para cambiar el rendimiento de una colección too5 Hola, 000 unidades de solicitud por segundo sin aprovisionamiento RU por minuto utilizando Hola .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="052e5-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="052e5-155">Escenarios de buen ajuste</span><span class="sxs-lookup"><span data-stu-id="052e5-155">Good fit scenarios</span></span>

<span data-ttu-id="052e5-156">En esta sección, proporcionamos información general de escenarios de buen ajuste para habilitar unidades de solicitud por minuto.</span><span class="sxs-lookup"><span data-stu-id="052e5-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="052e5-157">**Entorno de desarrollo y pruebas:** buen ajuste.</span><span class="sxs-lookup"><span data-stu-id="052e5-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="052e5-158">Durante la fase de desarrollo de hello, si va a probar la aplicación con distintas cargas de trabajo, RU/m puede proporcionar flexibilidad de hello en esta fase.</span><span class="sxs-lookup"><span data-stu-id="052e5-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="052e5-159">Mientras hello [emulador](local-emulator.md) es una base de datos de Azure Cosmos tootest de excelente herramienta gratuita.</span><span class="sxs-lookup"><span data-stu-id="052e5-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="052e5-160">Sin embargo si desea toostart en un entorno de nube, tendrá una gran flexibilidad con RU/m para sus necesidades de rendimiento "ad hoc".</span><span class="sxs-lookup"><span data-stu-id="052e5-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="052e5-161">Pasará más tiempo desarrollando que preocupándose de las necesidades de rendimiento al principio.</span><span class="sxs-lookup"><span data-stu-id="052e5-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="052e5-162">Se recomienda empezar con el aprovisionamiento de hello mínimo RU/s y habilitar RU/m.</span><span class="sxs-lookup"><span data-stu-id="052e5-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="052e5-163">**Necesidades de granularidad de minuto con picos impredecibles:** buen ajuste. Ahorro: 25-75 %.</span><span class="sxs-lookup"><span data-stu-id="052e5-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="052e5-164">Hemos observado una gran mejora con respecto a RU/m, estando en dicho grupo la mayoría de los escenarios de producción.</span><span class="sxs-lookup"><span data-stu-id="052e5-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="052e5-165">Si tiene una carga de trabajo de IoT tiene pico varias veces en un minuto, si dispone de las consultas se ejecutan cuando el sistema realiza insertar masivamente en hello mismo tiempo, necesitará capacidad adicional para necesidades de handeling picos.</span><span class="sxs-lookup"><span data-stu-id="052e5-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="052e5-166">Recomendamos optimizar sus necesidades de recursos aplicando nuestro enfoque paso a paso a continuación.</span><span class="sxs-lookup"><span data-stu-id="052e5-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Gráfico donde se muestra el consumo de la solicitud en una granularidad de cinco minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="052e5-168">*Ilustración: prueba comparativa de consumo de RU*</span><span class="sxs-lookup"><span data-stu-id="052e5-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="052e5-169">**Tranquilidad:** buen ajuste. Ahorro: 10-20 %.</span><span class="sxs-lookup"><span data-stu-id="052e5-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="052e5-170">A veces, simplemente desea toohave tranquilidad y no preocuparse sobre los posibles picos de actividad y la limitación.</span><span class="sxs-lookup"><span data-stu-id="052e5-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="052e5-171">Esta característica es Hola right uno automáticamente.</span><span class="sxs-lookup"><span data-stu-id="052e5-171">This feature is hello right one for you.</span></span> <span data-ttu-id="052e5-172">En ese caso, recomendamos habilitar RU/m y, de un modo ligeramente menos intenso, su aprovisionamiento por segundo.</span><span class="sxs-lookup"><span data-stu-id="052e5-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="052e5-173">En este caso es diferente de hello anteriormente como no intentará hacerlo toooptimize activamente el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="052e5-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="052e5-174">Esto es más como una mentalidad de “limitación cero” que adopta.</span><span class="sxs-lookup"><span data-stu-id="052e5-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="052e5-175">Las operaciones críticas con necesidades de "ad hoc": en ocasiones, se recomienda tooonly permiten operaciones críticas acceso RU/m presupuesto para no obtener presupuesto Hola consumir por "ad hoc" o menos importantes operaciones.</span><span class="sxs-lookup"><span data-stu-id="052e5-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="052e5-176">Que se pueden definir fácilmente en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="052e5-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="052e5-177">Uso de hello métricas portal toooptimize costo y el rendimiento</span><span class="sxs-lookup"><span data-stu-id="052e5-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="052e5-178">**En las próximas semanas hello, se desarrollará más contenido de hello alrededor RUs consumo minuto toooptimize que las necesidades de rendimiento de supervisión.**</span><span class="sxs-lookup"><span data-stu-id="052e5-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="052e5-179">A través de las métricas de portal de hello, puede ver la cantidad de segundos de RU regulares utilizas frente a RU minutos.</span><span class="sxs-lookup"><span data-stu-id="052e5-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="052e5-180">La supervisión de estas métricas debe ayudarle a optimizar su aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="052e5-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="052e5-181">Se recomienda un enfoque de paso a paso acerca de cómo toouse RU/m tooyour ventaja.</span><span class="sxs-lookup"><span data-stu-id="052e5-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="052e5-182">Para cada paso, debe tener una visión general del consumo de hello RU que representa un ciclo completo de la carga de trabajo (podría ser horas, días, o incluso semanas), obtendrá información sobre la utilización de Hola de lo que se aprovisiona.</span><span class="sxs-lookup"><span data-stu-id="052e5-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="052e5-183">principio de Hello detrás de este enfoque es toomake el aprovisionamiento de rendimiento como cerrar como posibles tooa aprovisionamiento punto que coincida con los rendimiento de los siguientes criterios.</span><span class="sxs-lookup"><span data-stu-id="052e5-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Gráfico donde se muestra el consumo de la solicitud en una granularidad de cinco minutos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="052e5-185">toounderstand Hola aprovisionamiento punto óptimo para la carga de trabajo, debe toounderstand:</span><span class="sxs-lookup"><span data-stu-id="052e5-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="052e5-186">Patrones de consumo: ¿picos inexistentes, poco frecuentes o sostenidos?</span><span class="sxs-lookup"><span data-stu-id="052e5-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="052e5-187">¿Picos pequeños (doble de media), medios o grandes (más de 10 veces de media)?</span><span class="sxs-lookup"><span data-stu-id="052e5-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="052e5-188">Porcentaje de solicitudes limitadas: ¿se siente cómodo en caso de tener un poco de limitación?</span><span class="sxs-lookup"><span data-stu-id="052e5-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="052e5-189">Si es así, ¿en qué medida?</span><span class="sxs-lookup"><span data-stu-id="052e5-189">If so, by how much?</span></span> 

<span data-ttu-id="052e5-190">Cuando haya identificado ¿cuáles son los objetivos, es posible que pueda tooget cuanto más se acerque toohello óptimo de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="052e5-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="052e5-191">tooassist, queremos tooprovide una orientación general sobre cómo toooptimize su aprovisionamiento según su consumo RU/m.</span><span class="sxs-lookup"><span data-stu-id="052e5-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="052e5-192">Esta guía no aplica tooall tipo de cargas de trabajo, pero se basa en el conocimiento de la vista previa privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="052e5-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="052e5-193">Puede que cambiemos estas líneas base a medida que obtenemos más información:</span><span class="sxs-lookup"><span data-stu-id="052e5-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="052e5-194">RU/m % uso</span><span class="sxs-lookup"><span data-stu-id="052e5-194">RU/m % utilization</span></span>|<span data-ttu-id="052e5-195">Grado de uso de RU/m</span><span class="sxs-lookup"><span data-stu-id="052e5-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="052e5-196">Medidas recomendadas para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="052e5-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="052e5-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="052e5-197">0-1%</span></span>|<span data-ttu-id="052e5-198">En uso</span><span class="sxs-lookup"><span data-stu-id="052e5-198">Under utilization</span></span>|<span data-ttu-id="052e5-199">Reducir RU/s tooconsume más RU/m</span><span class="sxs-lookup"><span data-stu-id="052e5-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="052e5-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="052e5-200">1-10%</span></span>|<span data-ttu-id="052e5-201">Uso correcto</span><span class="sxs-lookup"><span data-stu-id="052e5-201">Healthy use</span></span>|<span data-ttu-id="052e5-202">Mantener hello mismo aprovisionamiento nivel</span><span class="sxs-lookup"><span data-stu-id="052e5-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="052e5-203">Por encima del 10%</span><span class="sxs-lookup"><span data-stu-id="052e5-203">Above 10%</span></span>|<span data-ttu-id="052e5-204">Uso excesivo</span><span class="sxs-lookup"><span data-stu-id="052e5-204">Over utilization</span></span>|<span data-ttu-id="052e5-205">Aumentar RU/s toorely menos en RU/m.</span><span class="sxs-lookup"><span data-stu-id="052e5-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="052e5-206">Seleccione qué operaciones pueden consumir el presupuesto de hello RU/m</span><span class="sxs-lookup"><span data-stu-id="052e5-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="052e5-207">En el nivel de solicitud, puede también habilitar o deshabilitar la solicitud de RU/m presupuesto tooserve Hola independientemente del tipo de operación.</span><span class="sxs-lookup"><span data-stu-id="052e5-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="052e5-208">Si se consume regular aprovisionado presupuesto de RUs/seg. y solicitud de hello no puede usar el presupuesto de hello RU/m, se limitarán esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="052e5-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="052e5-209">De forma predeterminada, el presupuesto de RU/m atiende todas las solicitudes si se activa el presupuesto de rendimiento de RU/m.</span><span class="sxs-lookup"><span data-stu-id="052e5-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="052e5-210">Este es un fragmento de código para deshabilitar la asignación de RU/m con hello API de documentos para las operaciones CRUD y consulta.</span><span class="sxs-lookup"><span data-stu-id="052e5-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="052e5-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="052e5-211">Next steps</span></span>

<span data-ttu-id="052e5-212">En este artículo hemos descrito el funcionamiento de las particiones en Azure Cosmos DB, cómo crear colecciones particionadas y cómo elegir una buena clave de partición para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="052e5-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="052e5-213">Realice pruebas de escala y de rendimiento con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="052e5-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="052e5-214">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md) para ver ejemplos.</span><span class="sxs-lookup"><span data-stu-id="052e5-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="052e5-215">Comenzar a codificar con hello [SDK](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="052e5-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="052e5-216">Información sobre el [procesamiento aprovisionado](request-units.md) en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="052e5-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

