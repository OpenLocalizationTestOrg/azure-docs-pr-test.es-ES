---
title: Niveles de rendimiento en de la API de DocumentDB | Microsoft Docs
description: "Obtenga información sobre cómo los niveles de rendimiento de la API de DocumentDB le permiten reservar capacidad de proceso para cada contenedor."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d4733e57eb760dbb8e8ca96f6ba55671d1742f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="d1473-103">Retirada de los niveles de rendimiento S1, S2 y S3</span><span class="sxs-lookup"><span data-stu-id="d1473-103">Retiring the S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d1473-104">Los niveles de rendimiento S1, S2 y S3 descritos en este artículo se han retirado y ya no están disponibles para las nuevas cuentas de API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d1473-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="d1473-105">Este artículo proporciona información general de los niveles de rendimiento S1, S2 y S3, y describe cómo se migrarán las colecciones que usan estos niveles de rendimiento a colecciones de partición única el 1 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="d1473-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span></span> <span data-ttu-id="d1473-106">Después de leer este artículo, podrá responder a las preguntas siguientes:</span><span class="sxs-lookup"><span data-stu-id="d1473-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="d1473-107">¿Por qué se han retirado los niveles de rendimiento S1, S2 y S3?</span><span class="sxs-lookup"><span data-stu-id="d1473-107">Why are the S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="d1473-108">¿Cómo se comparan las colecciones de partición única y con particiones con los niveles de rendimiento S1, S2 y S3?</span><span class="sxs-lookup"><span data-stu-id="d1473-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="d1473-109">¿Qué tengo que hacer para garantizar el acceso ininterrumpido a mis datos?</span><span class="sxs-lookup"><span data-stu-id="d1473-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="d1473-110">¿Cómo cambiará mi colección después de la migración?</span><span class="sxs-lookup"><span data-stu-id="d1473-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="d1473-111">¿Cómo cambiará mi facturación después migrar a colecciones de partición única?</span><span class="sxs-lookup"><span data-stu-id="d1473-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="d1473-112">¿Qué ocurre si necesito más de 10 GB de almacenamiento?</span><span class="sxs-lookup"><span data-stu-id="d1473-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="d1473-113">¿Puedo cambiar entre los niveles de rendimiento S1, S2 y S3 antes del 1 de agosto de 2017?</span><span class="sxs-lookup"><span data-stu-id="d1473-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="d1473-114">¿Cómo puedo saber cuándo ha migrado mi colección?</span><span class="sxs-lookup"><span data-stu-id="d1473-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="d1473-115">¿Cómo migro de los niveles de rendimiento S1, S2 y S3 a las colecciones de partición única por mí mismo?</span><span class="sxs-lookup"><span data-stu-id="d1473-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="d1473-116">¿Cómo me afecta si soy un cliente de EA?</span><span class="sxs-lookup"><span data-stu-id="d1473-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="d1473-117">¿Por qué se han retirado los niveles de rendimiento S1, S2 y S3?</span><span class="sxs-lookup"><span data-stu-id="d1473-117">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="d1473-118">Los niveles de rendimiento S1, S2 y S3 no ofrecen la flexibilidad que proporcionan las colecciones de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d1473-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="d1473-119">Con los niveles de rendimiento S1, S2 y S3, tanto la capacidad de rendimiento como la de almacenamiento están preestablecidas y no ofrecen elasticidad.</span><span class="sxs-lookup"><span data-stu-id="d1473-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="d1473-120">Ahora Azure Cosmos DB ofrece la capacidad para personalizar su rendimiento y almacenamiento, lo que ofrece mucha más flexibilidad para el escalado a medida que cambien sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="d1473-120">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="d1473-121">¿Cómo se comparan las colecciones de partición única y con particiones con los niveles de rendimiento S1, S2 y S3?</span><span class="sxs-lookup"><span data-stu-id="d1473-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="d1473-122">En la tabla siguiente se comparan las opciones de rendimiento y almacenamiento disponibles en las colecciones de partición única, las colecciones con particiones y los niveles de rendimiento S1, S2 y S3.</span><span class="sxs-lookup"><span data-stu-id="d1473-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="d1473-123">Este es un ejemplo para la región Este de EE. UU. - 2:</span><span class="sxs-lookup"><span data-stu-id="d1473-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="d1473-124">Colección con particiones</span><span class="sxs-lookup"><span data-stu-id="d1473-124">Partitioned collection</span></span>|<span data-ttu-id="d1473-125">Colección de partición única</span><span class="sxs-lookup"><span data-stu-id="d1473-125">Single partition collection</span></span>|<span data-ttu-id="d1473-126">S1</span><span class="sxs-lookup"><span data-stu-id="d1473-126">S1</span></span>|<span data-ttu-id="d1473-127">S2</span><span class="sxs-lookup"><span data-stu-id="d1473-127">S2</span></span>|<span data-ttu-id="d1473-128">S3</span><span class="sxs-lookup"><span data-stu-id="d1473-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="d1473-129">Rendimiento máximo</span><span class="sxs-lookup"><span data-stu-id="d1473-129">Maximum throughput</span></span>|<span data-ttu-id="d1473-130">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="d1473-130">Unlimited</span></span>|<span data-ttu-id="d1473-131">10 000 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-131">10K RU/s</span></span>|<span data-ttu-id="d1473-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-132">250 RU/s</span></span>|<span data-ttu-id="d1473-133">1000 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-133">1 K RU/s</span></span>|<span data-ttu-id="d1473-134">2500 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="d1473-135">Rendimiento mínimo</span><span class="sxs-lookup"><span data-stu-id="d1473-135">Minimum throughput</span></span>|<span data-ttu-id="d1473-136">2500 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-136">2.5K RU/s</span></span>|<span data-ttu-id="d1473-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-137">400 RU/s</span></span>|<span data-ttu-id="d1473-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-138">250 RU/s</span></span>|<span data-ttu-id="d1473-139">1000 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-139">1 K RU/s</span></span>|<span data-ttu-id="d1473-140">2500 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="d1473-141">Almacenamiento máximo</span><span class="sxs-lookup"><span data-stu-id="d1473-141">Maximum storage</span></span>|<span data-ttu-id="d1473-142">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="d1473-142">Unlimited</span></span>|<span data-ttu-id="d1473-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="d1473-143">10 GB</span></span>|<span data-ttu-id="d1473-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="d1473-144">10 GB</span></span>|<span data-ttu-id="d1473-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="d1473-145">10 GB</span></span>|<span data-ttu-id="d1473-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="d1473-146">10 GB</span></span>|
|<span data-ttu-id="d1473-147">Precio (mensual)</span><span class="sxs-lookup"><span data-stu-id="d1473-147">Price (monthly)</span></span>|<span data-ttu-id="d1473-148">Rendimiento: 6 USD / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="d1473-149">Almacenamiento: 0,25 USD/GB</span><span class="sxs-lookup"><span data-stu-id="d1473-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="d1473-150">Rendimiento: 6 USD / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="d1473-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="d1473-151">Almacenamiento: 0,25 USD/GB</span><span class="sxs-lookup"><span data-stu-id="d1473-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="d1473-152">25 USD</span><span class="sxs-lookup"><span data-stu-id="d1473-152">$25 USD</span></span>|<span data-ttu-id="d1473-153">50 USD</span><span class="sxs-lookup"><span data-stu-id="d1473-153">$50 USD</span></span>|<span data-ttu-id="d1473-154">100 USD</span><span class="sxs-lookup"><span data-stu-id="d1473-154">$100 USD</span></span>|

<span data-ttu-id="d1473-155">¿Es un cliente de EA?</span><span class="sxs-lookup"><span data-stu-id="d1473-155">Are you an EA customer?</span></span> <span data-ttu-id="d1473-156">Si es así, consulte [¿Cómo me afecta si soy un cliente de EA?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="d1473-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="d1473-157">¿Qué tengo que hacer para garantizar el acceso ininterrumpido a mis datos?</span><span class="sxs-lookup"><span data-stu-id="d1473-157">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="d1473-158">Nada, Cosmos DB se ocupa de la migración por usted.</span><span class="sxs-lookup"><span data-stu-id="d1473-158">Nothing, Cosmos DB handles the migration for you.</span></span> <span data-ttu-id="d1473-159">Si tiene una colección de S1, S2 o S3, se migrará a una colección de partición única el 31 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="d1473-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="d1473-160">¿Cómo cambiará mi colección después de la migración?</span><span class="sxs-lookup"><span data-stu-id="d1473-160">How will my collection change after the migration?</span></span>

<span data-ttu-id="d1473-161">Si tiene una colección de S1, se migrará a una colección de partición única con un rendimiento de 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="d1473-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="d1473-162">400 RU/s es el rendimiento más bajo disponible con colecciones de partición única.</span><span class="sxs-lookup"><span data-stu-id="d1473-162">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="d1473-163">Sin embargo, el coste de 400 RU/s en la colección de partición única es aproximadamente el mismo que con la colección de S1 y 250 RU/s: por lo que no va a pagar por las 150 RU/s extra disponibles.</span><span class="sxs-lookup"><span data-stu-id="d1473-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="d1473-164">Si tiene una colección de S2, se migrará a una colección de partición única con 1000 RU/s.</span><span class="sxs-lookup"><span data-stu-id="d1473-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="d1473-165">No verá ningún cambio en su nivel de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d1473-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="d1473-166">Si tiene una colección de S3, se migrará a una colección de partición única con 2 500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="d1473-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="d1473-167">No verá ningún cambio en su nivel de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d1473-167">You will see no change to your throughput level.</span></span>

<span data-ttu-id="d1473-168">En todos estos casos, después de migrar la colección, podrá personalizar el nivel de rendimiento o escalar y reducir verticalmente según sea necesario para proporcionar un acceso de baja latencia a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d1473-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> <span data-ttu-id="d1473-169">Para cambiar el nivel de rendimiento después de migrar la colección, abra su cuenta de Cosmos DB en Azure Portal, haga clic en Escala, elija la colección y ajuste el nivel de rendimiento, como se muestra en la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="d1473-169">To change the throughput level after your collection has migrated, simply open your Cosmos DB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span></span>

![Escalado del rendimiento en Azure Portal](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-to-the-single-partition-collections"></a><span data-ttu-id="d1473-171">¿Cómo cambiará mi facturación después migrar a colecciones de partición única?</span><span class="sxs-lookup"><span data-stu-id="d1473-171">How will my billing change after I’m migrated to the single partition collections?</span></span>

<span data-ttu-id="d1473-172">Supongamos que tiene 10 colecciones S1 en la región Este de EE. UU. y 1 GB de almacenamiento para cada una, y las migra a 10 recopilaciones de partición única a 400 RU/seg. (el nivel mínimo).</span><span class="sxs-lookup"><span data-stu-id="d1473-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="d1473-173">Su factura tendrá el siguiente aspecto si mantiene las 10 colecciones de partición única un mes completo:</span><span class="sxs-lookup"><span data-stu-id="d1473-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![Cómo se comparan los precios de S1 para 10 colecciones con los precios de 10 colecciones que usan una colección de partición única](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="d1473-175">¿Qué ocurre si necesito más de 10 GB de almacenamiento?</span><span class="sxs-lookup"><span data-stu-id="d1473-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="d1473-176">Independientemente de si tiene una colección con un nivel de rendimiento S1, S2 o S3, o si tiene una colección de partición única, todos con 10 GB de almacenamiento disponibles, puede utilizar la herramienta de migración de datos de Cosmos DB para migrar los datos a una colección con particiones, con un almacenamiento prácticamente ilimitado.</span><span class="sxs-lookup"><span data-stu-id="d1473-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="d1473-177">Para más información acerca de las ventajas de una colección con particiones, consulte el tema sobre [particiones y escalado en Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d1473-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="d1473-178">Para más información sobre cómo migrar su colección de partición única o S1, S2, S3 a una colección con particiones, consulte [Migración desde colecciones de partición única a colecciones con varias particiones](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="d1473-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="d1473-179">¿Puedo cambiar entre los niveles de rendimiento S1, S2 y S3 antes del 1 de agosto de 2017?</span><span class="sxs-lookup"><span data-stu-id="d1473-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="d1473-180">Solo las cuentas existentes con los niveles S1, S2 y S3 podrán cambiar y modificar los niveles de rendimiento con el portal o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d1473-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span></span> <span data-ttu-id="d1473-181">A partir del 1 de agosto de 2017, los niveles de rendimiento S1, S2 y S3 ya no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="d1473-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="d1473-182">Si cambia de S1, S3 o S3 a una colección de partición única, no puede volver a los niveles de rendimiento S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="d1473-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="d1473-183">¿Cómo puedo saber cuándo ha migrado mi colección?</span><span class="sxs-lookup"><span data-stu-id="d1473-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="d1473-184">La migración se producirá el 31 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="d1473-184">The migration will occur on July 31, 2017.</span></span> <span data-ttu-id="d1473-185">Si tiene una colección que usa los niveles de rendimiento S1, S2 o S3, el equipo de Cosmos DB se comunicará con usted por correo electrónico antes de realizar la migración.</span><span class="sxs-lookup"><span data-stu-id="d1473-185">If you have a collection that uses the S1, S2 or S3 performance levels, the Cosmos DB team will contact you by email before the migration takes place.</span></span> <span data-ttu-id="d1473-186">Una vez completada el 1 de agosto de 2017, Azure Portal indicará que su colección utiliza el plan de tarifa Estándar.</span><span class="sxs-lookup"><span data-stu-id="d1473-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span></span>

![Procedimientos para confirmar que la colección se ha migrado al plan de tarifa Estándar](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="d1473-188">¿Cómo migro de los niveles de rendimiento S1, S2 y S3 a las colecciones de partición única por mí mismo?</span><span class="sxs-lookup"><span data-stu-id="d1473-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="d1473-189">Puede migrar de los niveles de rendimiento S1, S2 y S3 a colecciones de partición única con Azure Portal o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d1473-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span></span> <span data-ttu-id="d1473-190">Puede hacerlo por sí mismo antes del 1 de agosto para beneficiarse de las opciones de rendimiento flexible disponibles con colecciones de partición única, o bien migraremos las colecciones por usted el 31 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="d1473-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="d1473-191">**Para migrar a las colecciones de partición única con Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="d1473-191">**To migrate to single partition collections using the Azure portal**</span></span>

1. <span data-ttu-id="d1473-192">En [**Azure Portal**](https://portal.azure.com), haga clic en **Azure Cosmos DB** y seleccione la cuenta de Cosmos DB que se va a modificar.</span><span class="sxs-lookup"><span data-stu-id="d1473-192">In the [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select the Cosmos DB account to modify.</span></span> 
 
    <span data-ttu-id="d1473-193">Si **Azure Cosmos DB** no está en la barra de accesos, haga clic en >, vaya a **Bases de datos**, seleccione **Azure Cosmos DB** y luego seleccione la cuenta de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d1473-193">If **Azure Cosmos DB** is not on the Jumpbar, click >, scroll to **Databases**, select **Azure Cosmos DB**, and then select the DocumentDB account.</span></span>  

2. <span data-ttu-id="d1473-194">En el menú de recursos, en **Contenedores**, haga clic en **Escala**, seleccione la colección que desea modificar en la lista desplegable y luego haga clic en **Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="d1473-194">On the resource menu, under **Containers**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="d1473-195">Las cuentas con un rendimiento predefinido tienen un plan de tarifa de S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="d1473-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="d1473-196">En la hoja **Elegir su nivel de precios**, haga clic en **Estándar** para cambiar la capacidad de proceso definida por el usuario y luego haga clic en **Seleccionar** para guardar el cambio.</span><span class="sxs-lookup"><span data-stu-id="d1473-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span></span>

    ![Captura de pantalla de la hoja Configuración que muestra dónde cambiar el valor de rendimiento](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="d1473-198">En la hoja **Escala**, el **plan de tarifa** cambia a **Estándar** y el cuadro **Procesamiento (RU/s)** se muestra con un valor predeterminado de 400.</span><span class="sxs-lookup"><span data-stu-id="d1473-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="d1473-199">Establezca el rendimiento entre 400 y 10 000 [unidades de solicitud](request-units.md)/segundo (RU/s).</span><span class="sxs-lookup"><span data-stu-id="d1473-199">Set the throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="d1473-200">La opción **Factura mensual estimada** en la parte inferior de la página se actualiza automáticamente para ofrecer una estimación del costo mensual.</span><span class="sxs-lookup"><span data-stu-id="d1473-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="d1473-201">Cuando haya guardado los cambios y cambiado al plan de tarifa Estándar, no podrá revertir a los niveles de rendimiento S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="d1473-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="d1473-202">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="d1473-202">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="d1473-203">Si cree que necesita más rendimiento (superior a 10 000 RU/s) o espacio de almacenamiento (mayor que 10 GB), puede crear una colección con particiones.</span><span class="sxs-lookup"><span data-stu-id="d1473-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="d1473-204">Para migrar una colección de partición única a una colección con particiones, consulte [Migración desde colecciones de partición única a colecciones con varias particiones](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="d1473-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1473-205">El cambiar de S1, S2 o S3 a Estándar puede tardar hasta 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="d1473-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="d1473-206">**Para migrar a colecciones de partición única con el SDK de .NET**</span><span class="sxs-lookup"><span data-stu-id="d1473-206">**To migrate to single partition collections using the .NET SDK**</span></span>

<span data-ttu-id="d1473-207">Otra opción para cambiar los niveles de rendimiento de las colecciones es a través de nuestros SDK.</span><span class="sxs-lookup"><span data-stu-id="d1473-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="d1473-208">En esta sección solo se trata el cambio del nivel de rendimiento de una colección mediante la [API de .NET de DocumentDB](documentdb-sdk-dotnet.md), pero el proceso es similar para otros SDK.</span><span class="sxs-lookup"><span data-stu-id="d1473-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but the process is similar for our other SDKs.</span></span>

<span data-ttu-id="d1473-209">A continuación se muestra un fragmento de código para cambiar el rendimiento de la colección a 5 000 unidades de solicitud por segundo:</span><span class="sxs-lookup"><span data-stu-id="d1473-209">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```C#
    //Fetch the resource to be updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set the throughput to 5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes to the database by replacing the original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="d1473-210">Visite [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) para ver más ejemplos y obtener más información sobre nuestros métodos de oferta:</span><span class="sxs-lookup"><span data-stu-id="d1473-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="d1473-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="d1473-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="d1473-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="d1473-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="d1473-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="d1473-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="d1473-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="d1473-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="d1473-215">¿Cómo me afecta si soy un cliente de EA?</span><span class="sxs-lookup"><span data-stu-id="d1473-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="d1473-216">El precio para los clientes de EA estará protegido hasta el final de su contrato actual.</span><span class="sxs-lookup"><span data-stu-id="d1473-216">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1473-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1473-217">Next steps</span></span>
<span data-ttu-id="d1473-218">Para obtener más información sobre los precios y la administración de datos con Azure Cosmos DB, consulte estos recursos:</span><span class="sxs-lookup"><span data-stu-id="d1473-218">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="d1473-219">[Partición de datos en Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d1473-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="d1473-220">Información sobre la diferencia entre un contenedor de partición única y contenedores con particiones, así como sugerencias sobre cómo implementar una estrategia de particiones para escalar sin problemas.</span><span class="sxs-lookup"><span data-stu-id="d1473-220">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="d1473-221">[Precios de Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d1473-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="d1473-222">Aprenda sobre los costes de rendimiento del aprovisionamiento y el consumo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d1473-222">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="d1473-223">[Unidades de solicitud](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="d1473-223">[Request units](request-units.md).</span></span> <span data-ttu-id="d1473-224">Información sobre el consumo de rendimiento para diferentes tipos de operaciones; por ejemplo, lectura, escritura o consulta.</span><span class="sxs-lookup"><span data-stu-id="d1473-224">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
