---
title: "Creación de particiones de los servicios de Service Fabric | Microsoft Docs"
description: "Describe cómo crear particiones en los servicios con estado de Service Fabric. Particiones permiten el almacenamiento de datos en las máquinas locales de forma que los datos y el proceso pueden escalarse juntos."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 3c1e80305cb65f41a6981b99f69e8b87f89599ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="0ef77-104">Partición de Reliable Services de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ef77-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="0ef77-105">Este artículo proporciona una introducción a los conceptos básicos de la creación de particiones en Reliable Services de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ef77-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="0ef77-106">El código fuente que se usa en el artículo también está disponible en [Github](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="0ef77-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="0ef77-107">Creación de particiones</span><span class="sxs-lookup"><span data-stu-id="0ef77-107">Partitioning</span></span>
<span data-ttu-id="0ef77-108">La creación de particiones no es exclusiva de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ef77-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="0ef77-109">De hecho, es una función básica de la compilación de servicios escalables.</span><span class="sxs-lookup"><span data-stu-id="0ef77-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="0ef77-110">En un sentido amplio, podemos considerar la creación de particiones como un estado de división (datos) y procesamiento en unidades accesibles más pequeñas para mejorar el rendimiento y escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="0ef77-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="0ef77-111">Una forma conocida de partición es la [partición de datos][wikipartition] también conocida como particionamiento.</span><span class="sxs-lookup"><span data-stu-id="0ef77-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="0ef77-112">Partición de los servicios sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ef77-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="0ef77-113">Para los servicios sin estado, puede pensar en una partición como en una unidad lógica que contiene una o varias instancias de un servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="0ef77-114">La ilustración 1 muestra un servicio sin estado con cinco instancias distribuidas en un clúster con una partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Servicio sin estado](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="0ef77-116">En realidad hay dos tipos de soluciones de servicios sin estado.</span><span class="sxs-lookup"><span data-stu-id="0ef77-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="0ef77-117">La primera corresponde a un servicio que conserva su estado de forma externa, por ejemplo en una Base de datos SQL de Azure (como un sitio web que almacena la información de sesión y los datos).</span><span class="sxs-lookup"><span data-stu-id="0ef77-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="0ef77-118">La segunda corresponde a servicios solo de procesamiento (como una calculadora o un generador de imágenes en miniatura) que no administran ningún estado persistente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="0ef77-119">En cualquier caso, la partición de un servicio sin estado es un escenarios muy poco frecuente en el que la escalabilidad y la disponibilidad normalmente se consiguen agregando más instancias.</span><span class="sxs-lookup"><span data-stu-id="0ef77-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="0ef77-120">Las únicas ocasiones en las que posiblemente quiera plantearse varias particiones para las instancias de servicios sin estado es cuando tenga que satisfacer solicitudes de enrutamiento especiales.</span><span class="sxs-lookup"><span data-stu-id="0ef77-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="0ef77-121">Por ejemplo, piense en un caso en el que los usuarios con identificadores dentro de un intervalo específico deberán ser atendidos únicamente por una instancia de servicio determinada.</span><span class="sxs-lookup"><span data-stu-id="0ef77-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="0ef77-122">Otro ejemplo de cuándo se puede particionar un servicio sin estado es cuando tiene un back-end con particiones, por ejemplo, una base de datos SQL particionada, y desea controlar qué instancia del servicio debe escribir en la partición de la base de datos o realizar otro trabajo de preparación en el servicio sin estado que requiera la misma información de partición que se usa en el back-end.</span><span class="sxs-lookup"><span data-stu-id="0ef77-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="0ef77-123">Estos tipos de escenarios también se pueden resolver de maneras diferentes y no requieren necesariamente el particionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="0ef77-124">El resto de este tutorial se centra en los servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="0ef77-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="0ef77-125">Partición de los servicios con estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ef77-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="0ef77-126">Service Fabric ofrece una manera idónea para particionar el estado (datos) y facilitar el desarrollo de servicios con estado escalables.</span><span class="sxs-lookup"><span data-stu-id="0ef77-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="0ef77-127">Conceptualmente, puede pensar en una partición de un servicio con estado como una unidad de escalado muy confiable gracias a las [réplicas](service-fabric-availability-services.md) que se distribuyen y se equilibran entre los nodos en un clúster.</span><span class="sxs-lookup"><span data-stu-id="0ef77-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="0ef77-128">En el contexto de los servicios con estado de Service Fabric, la creación de particiones es el proceso de determinar que una partición de servicio específica es responsable de una parte de todo el estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="0ef77-129">(Como se mencionó anteriormente, una partición es un conjunto de [réplicas](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="0ef77-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="0ef77-130">Una gran ventaja de Service Fabric es que coloca las particiones en nodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0ef77-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="0ef77-131">Esto les permite crecer hasta el límite de recursos del nodo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="0ef77-132">A medida que los datos crecen, las particiones también crecen y Service Fabric vuelve a equilibrar las particiones entre los nodos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="0ef77-133">Esto garantiza el uso continuado y eficaz de los recursos de hardware.</span><span class="sxs-lookup"><span data-stu-id="0ef77-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="0ef77-134">Como ejemplo, digamos que comienza con un clúster de 5 nodos y un servicio configurado para tener 10 particiones y un destino de tres réplicas.</span><span class="sxs-lookup"><span data-stu-id="0ef77-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="0ef77-135">En este caso, Service Fabric equilibrará y distribuirá las réplicas en el clúster y acabara con dos [réplicas](service-fabric-availability-services.md) principales por nodo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="0ef77-136">Si necesita escalar horizontalmente el clúster a 10 nodos, Service Fabric volverá a equilibrar las [réplicas](service-fabric-availability-services.md) principales en los 10 nodos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="0ef77-137">Del mismo modo, si vuelve a 5 nodos, Service Fabric volverá a equilibrar todas las réplicas en los 5 nodos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="0ef77-138">La ilustración 2 muestra la distribución de 10 particiones antes y después de escalar el clúster.</span><span class="sxs-lookup"><span data-stu-id="0ef77-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![Servicio con estado](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="0ef77-140">Como resultado, se logra el escalado horizontal ya que las solicitudes de los clientes se distribuyen entre los equipos, mejora el rendimiento general de la aplicación y se reduce la contención en el acceso a los fragmentos de datos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="0ef77-141">Plan para la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="0ef77-141">Plan for partitioning</span></span>
<span data-ttu-id="0ef77-142">Antes de implementar un servicio, debe considerar siempre la estrategia de particiones que se necesita para el escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="0ef77-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out.</span></span> <span data-ttu-id="0ef77-143">Hay diferentes maneras, pero todas ellas se centran en lo que la aplicación necesita lograr.</span><span class="sxs-lookup"><span data-stu-id="0ef77-143">There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="0ef77-144">Veamos algunos de los aspectos más importantes dentro del contexto de este artículo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-144">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="0ef77-145">Un buen método es pensar primero en la estructura del estado que es necesario particionar.</span><span class="sxs-lookup"><span data-stu-id="0ef77-145">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="0ef77-146">Veamos un sencillo ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-146">Let's take a simple example.</span></span> <span data-ttu-id="0ef77-147">Si tuviera que crear un servicio para un sondeo de ámbito regional, puede crear una partición para cada ciudad de la región.</span><span class="sxs-lookup"><span data-stu-id="0ef77-147">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="0ef77-148">A continuación, puede almacenar los votos de cada persona de la ciudad en la partición correspondiente a esa ciudad.</span><span class="sxs-lookup"><span data-stu-id="0ef77-148">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="0ef77-149">La ilustración 3 muestra un conjunto de usuarios y la ciudad en la que residen.</span><span class="sxs-lookup"><span data-stu-id="0ef77-149">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![Partición simple](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="0ef77-151">Como la población de las ciudades varía mucho, puede terminar con algunas particiones que contienen grandes cantidades de datos (por ejemplo, Seattle) y otras particiones con muy poco estado (por ejemplo, Kirkland).</span><span class="sxs-lookup"><span data-stu-id="0ef77-151">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="0ef77-152">¿En qué afecta tener particiones con cantidades de estado desiguales?</span><span class="sxs-lookup"><span data-stu-id="0ef77-152">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="0ef77-153">Si vuelve a pensar en el ejemplo, verá fácilmente que la partición que contiene los votos de Seattle tendrá más tráfico que la de Kirkland.</span><span class="sxs-lookup"><span data-stu-id="0ef77-153">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="0ef77-154">De forma predeterminada, Service Fabric se asegura de que hay aproximadamente el mismo número de réplicas principales y secundarias en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-154">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="0ef77-155">Por lo que puede encontrarse con nodos que contienen réplicas que atienden más tráfico y otros que atienden de menos tráfico.</span><span class="sxs-lookup"><span data-stu-id="0ef77-155">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="0ef77-156">Es preferible evitar puntos con tráfico intenso y puntos con apenas tráfico como estos en un clúster.</span><span class="sxs-lookup"><span data-stu-id="0ef77-156">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="0ef77-157">Para ello, debe hacer dos cosas desde el punto de vista de la creación de particiones:</span><span class="sxs-lookup"><span data-stu-id="0ef77-157">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="0ef77-158">Pruebe a particionar el estado para que se distribuya uniformemente en todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="0ef77-158">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="0ef77-159">Notifique la carga de cada una de las réplicas del servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-159">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="0ef77-160">(Para más información al respecto, consulte este artículo sobre [métricas y carga](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="0ef77-160">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="0ef77-161">Service Fabric ofrece la posibilidad de notificar la carga consumida por los servicios, como la cantidad de memoria o el número de registros.</span><span class="sxs-lookup"><span data-stu-id="0ef77-161">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="0ef77-162">En base a las métricas notificadas, Service Fabric detecta que algunas particiones atienden cargas mayores que otras y vuelve a equilibrar el clúster moviendo las réplicas a nodos más adecuados, de modo que en general ningún nodo resulta sobrecargado.</span><span class="sxs-lookup"><span data-stu-id="0ef77-162">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="0ef77-163">A veces, no es posible saber la cantidad de datos que habrá en una partición determinada.</span><span class="sxs-lookup"><span data-stu-id="0ef77-163">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="0ef77-164">Por ello se recomienda realizar ambas acciones: primero adoptar una estrategia para distribuir los datos uniformemente entre las particiones y, después, crear informes de la carga.</span><span class="sxs-lookup"><span data-stu-id="0ef77-164">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="0ef77-165">El primer método evita situaciones como las descritas en el ejemplo de la votación, mientras que el segundo ayuda a suavizar las diferencias temporales en el acceso o la carga con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-165">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="0ef77-166">Otro aspecto de la planeación de las particiones es elegir el número correcto de particiones para comenzar.</span><span class="sxs-lookup"><span data-stu-id="0ef77-166">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="0ef77-167">Desde la perspectiva de Service Fabric, nada le impide comenzar con un número de particiones mayor del previsto para su escenario.</span><span class="sxs-lookup"><span data-stu-id="0ef77-167">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="0ef77-168">De hecho, adoptar el número máximo de particiones es un enfoque válido.</span><span class="sxs-lookup"><span data-stu-id="0ef77-168">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="0ef77-169">En raras ocasiones puede acabar necesitando más particiones que las elegidas inicialmente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-169">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="0ef77-170">En estos casos, como no se puede cambiar el número de particiones después, tendría que aplicar algunos métodos de partición avanzados, como crear una nueva instancia de servicio del mismo tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-170">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="0ef77-171">También tendrá que implementar alguna lógica del lado cliente que enruta las solicitudes a la instancia de servicio correcta, en base al conocimiento del cliente que debe mantener el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-171">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="0ef77-172">Otra consideración a la hora de planear las particiones es cuáles son los recursos disponibles en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-172">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="0ef77-173">Como es necesario almacenar el estado y acceder a él, depende de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ef77-173">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="0ef77-174">Límites del ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="0ef77-174">Network bandwidth limits</span></span>
* <span data-ttu-id="0ef77-175">Límites de la memoria del sistema</span><span class="sxs-lookup"><span data-stu-id="0ef77-175">System memory limits</span></span>
* <span data-ttu-id="0ef77-176">Límites del almacenamiento en disco</span><span class="sxs-lookup"><span data-stu-id="0ef77-176">Disk storage limits</span></span>

<span data-ttu-id="0ef77-177">Entonces, ¿qué ocurre si se producen restricciones de recursos en un clúster en ejecución?</span><span class="sxs-lookup"><span data-stu-id="0ef77-177">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="0ef77-178">La respuesta es que solo tiene que escalar horizontalmente el clúster para dar cabida a los nuevos requisitos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-178">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="0ef77-179">[La guía de planeación de la capacidad](service-fabric-capacity-planning.md) ofrece orientación para determinar cuántos nodos necesita su clúster.</span><span class="sxs-lookup"><span data-stu-id="0ef77-179">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="0ef77-180">Introducción a la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="0ef77-180">Get started with partitioning</span></span>
<span data-ttu-id="0ef77-181">En esta sección se describe cómo empezar a particionar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-181">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="0ef77-182">En primer lugar, Service Fabric ofrece tres esquemas de partición posibles:</span><span class="sxs-lookup"><span data-stu-id="0ef77-182">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="0ef77-183">Particiones de intervalo (también conocidas como UniformInt64Partition)</span><span class="sxs-lookup"><span data-stu-id="0ef77-183">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="0ef77-184">Particiones con nombre.</span><span class="sxs-lookup"><span data-stu-id="0ef77-184">Named partitioning.</span></span> <span data-ttu-id="0ef77-185">Las aplicaciones que usan este modelo suelen tener datos que se pueden incluir en cubos, dentro de un conjunto enlazado.</span><span class="sxs-lookup"><span data-stu-id="0ef77-185">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="0ef77-186">Algunos ejemplos habituales de campos de datos que se usan como claves de partición con nombre son regiones, códigos postales, grupos de clientes u otros límites empresariales.</span><span class="sxs-lookup"><span data-stu-id="0ef77-186">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="0ef77-187">Particiones de singleton.</span><span class="sxs-lookup"><span data-stu-id="0ef77-187">Singleton partitioning.</span></span> <span data-ttu-id="0ef77-188">Las particiones de singleton se usan normalmente cuando el servicio no requiere ningún enrutamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="0ef77-188">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="0ef77-189">Por ejemplo, los servicios sin estado usan este esquema de partición de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0ef77-189">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="0ef77-190">Los esquemas de particiones con nombre y de singleton son formas especiales de particiones de intervalos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-190">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="0ef77-191">De forma predeterminada, las plantillas de Visual Studio para Service Fabric usan las particiones de intervalo, ya que es el esquema más habitual y útil.</span><span class="sxs-lookup"><span data-stu-id="0ef77-191">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="0ef77-192">El resto de este artículo se centra en el esquema de particiones de intervalo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-192">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="0ef77-193">Esquema de particiones de intervalo</span><span class="sxs-lookup"><span data-stu-id="0ef77-193">Ranged partitioning scheme</span></span>
<span data-ttu-id="0ef77-194">Se usa para especificar un intervalo de enteros (identificado por una clave baja y otra alta) y un número de particiones (n).</span><span class="sxs-lookup"><span data-stu-id="0ef77-194">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="0ef77-195">Crea n particiones, cada una de ellas responsable de un subintervalo no superpuesto del intervalo de claves de partición general.</span><span class="sxs-lookup"><span data-stu-id="0ef77-195">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="0ef77-196">Por ejemplo: un esquema de partición de intervalo con una clave baja 0, una clave alta de 99 y un recuento de 4 crearía 4 particiones, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ef77-196">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Creación de particiones por rangos](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="0ef77-198">Un enfoque habitual es crear un hash basado en una clave única dentro del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-198">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="0ef77-199">Algunos ejemplos comunes de claves son un número de identificación de vehículo (VIN), identificación de empleado o una cadena única.</span><span class="sxs-lookup"><span data-stu-id="0ef77-199">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="0ef77-200">Con esa clave única, se genera un código hash, módulo del intervalo de claves, para usarlo como clave.</span><span class="sxs-lookup"><span data-stu-id="0ef77-200">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="0ef77-201">Puede especificar los límites superior e inferior del intervalo de claves permitido.</span><span class="sxs-lookup"><span data-stu-id="0ef77-201">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="0ef77-202">Selección de un algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="0ef77-202">Select a hash algorithm</span></span>
<span data-ttu-id="0ef77-203">Una parte importante de los algoritmos hash es seleccionar su algoritmo hash.</span><span class="sxs-lookup"><span data-stu-id="0ef77-203">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="0ef77-204">Una cuestión que se debe tener en cuenta es si el objetivo es agrupar claves similares próximas entre sí (algoritmos hash sensibles a la ubicación) o si la actividad se debería distribuir ampliamente entre todas las particiones (algoritmos hash de distribución), que suele ser lo más común.</span><span class="sxs-lookup"><span data-stu-id="0ef77-204">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="0ef77-205">Las características de un buen algoritmo hash de distribución son que sea fácil de calcular, que tenga pocas colisiones y que distribuya las claves uniformemente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-205">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="0ef77-206">Un buen ejemplo de un algoritmo hash eficaz es el algoritmo hash [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) .</span><span class="sxs-lookup"><span data-stu-id="0ef77-206">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="0ef77-207">Un buen recurso para las opciones de algoritmo de código hash generales es [la página de Wikipedia sobre las funciones hash](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="0ef77-207">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="0ef77-208">Creación de un servicio con estado con varias particiones</span><span class="sxs-lookup"><span data-stu-id="0ef77-208">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="0ef77-209">Vamos a crear su primer servicio con estado confiable con varias particiones.</span><span class="sxs-lookup"><span data-stu-id="0ef77-209">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="0ef77-210">En este ejemplo, creará una aplicación muy sencilla para almacenar todos los apellidos que comienzan con la misma letra en la misma partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-210">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="0ef77-211">Antes de escribir ningún código, tiene que pensar en las particiones y en las claves de partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-211">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="0ef77-212">Necesita 26 particiones, una para cada letra del alfabeto, pero ¿qué hay de las claves inferiores y superiores?</span><span class="sxs-lookup"><span data-stu-id="0ef77-212">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="0ef77-213">Puesto que literalmente queremos tener una partición por cada letra, podemos usar 0 como clave inferior y 25 como clave superior porque cada letra es su propia clave.</span><span class="sxs-lookup"><span data-stu-id="0ef77-213">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="0ef77-214">Este es un escenario simplificado porque, en realidad, la distribución sería desigual.</span><span class="sxs-lookup"><span data-stu-id="0ef77-214">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="0ef77-215">Los apellidos que comienzan por las letras S o M son más comunes que los que comienzan por X o Y.</span><span class="sxs-lookup"><span data-stu-id="0ef77-215">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="0ef77-216">Abra **Visual Studio** > **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="0ef77-216">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="0ef77-217">En el cuadro de diálogo **Nuevo proyecto** , elija la aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ef77-217">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="0ef77-218">Llame al proyecto AlphabetPartitions.</span><span class="sxs-lookup"><span data-stu-id="0ef77-218">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="0ef77-219">En el cuadro de diálogo **Crear un servicio**, elija el servicio **Con estado** y llámelo Alphabet.Processing, tal y como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-219">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
       <span data-ttu-id="0ef77-220">![Cuadro de diálogo de servicio nuevo en Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="0ef77-220">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="0ef77-221">Establezca el número de particiones.</span><span class="sxs-lookup"><span data-stu-id="0ef77-221">Set the number of partitions.</span></span> <span data-ttu-id="0ef77-222">Abra el archivo Applicationmanifest.xml de la carpeta ApplicationPackageRoot del proyecto AlphabetPartitions y actualice el parámetro Processing_PartitionCount con el valor 26, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ef77-222">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="0ef77-223">También tendrá que actualizar las propiedades LowKey y HighKey del elemento StatefulService del archivo ApplicationManifest.xml tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ef77-223">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="0ef77-224">Para que el servicio sea accesible, abra un punto de conexión en un puerto agregando el elemento punto de conexión de ServiceManifest.xml (que se encuentra en la carpeta PackageRoot) para el servicio Alphabet.Processing, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0ef77-224">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="0ef77-225">Ahora, el servicio está configurado para escuchar a un punto de conexión interno con 26 particiones.</span><span class="sxs-lookup"><span data-stu-id="0ef77-225">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="0ef77-226">A continuación, tiene que invalidar el método `CreateServiceReplicaListeners()` de la clase Processing.</span><span class="sxs-lookup"><span data-stu-id="0ef77-226">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ef77-227">Para este ejemplo, asumimos que está usando un HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="0ef77-227">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="0ef77-228">Para más información sobre la comunicación de Reliable Service, consulte [Modelo de comunicación de Reliable Service](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="0ef77-228">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="0ef77-229">Un patrón recomendado para la dirección URL que escucha una réplica es el siguiente formato: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="0ef77-229">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="0ef77-230">Por ello deberá configurar el agente de escucha de comunicación para escuchar en los puntos de conexión correctos y con este patrón.</span><span class="sxs-lookup"><span data-stu-id="0ef77-230">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="0ef77-231">Se pueden hospedar varias réplicas de este servicio en el mismo equipo, por lo que esta dirección debe ser única para la réplica.</span><span class="sxs-lookup"><span data-stu-id="0ef77-231">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="0ef77-232">Por este motivo, el identificador de la partición y el identificador de la réplica están incluidos en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="0ef77-232">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="0ef77-233">HttpListener puede escuchar varias direcciones en el mismo puerto siempre que el prefijo de dirección URL sea único.</span><span class="sxs-lookup"><span data-stu-id="0ef77-233">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="0ef77-234">El GUID adicional es para casos avanzados en los que las réplicas secundarias también escuchan solicitudes de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="0ef77-234">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="0ef77-235">En este caso, querrá asegurarse de que se usa una dirección única nueva al realizar la transición de principal a secundario para obligar a los clientes a volver a resolver la dirección.</span><span class="sxs-lookup"><span data-stu-id="0ef77-235">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="0ef77-236">'+' se usa como dirección aquí de forma que la réplica escucha en todos los hosts disponibles (IP, FQDM, localhost, etc.). El código siguiente muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0ef77-236">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="0ef77-237">También merece la pena tener en cuenta que la dirección URL publicada es ligeramente diferente del prefijo de URL de escucha.</span><span class="sxs-lookup"><span data-stu-id="0ef77-237">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="0ef77-238">La dirección URL de escucha se envía a HttpListener.</span><span class="sxs-lookup"><span data-stu-id="0ef77-238">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="0ef77-239">La dirección URL publicada es la dirección URL que se publica en el servicio de nombres de Service Fabric, que se usa para la detección de servicios.</span><span class="sxs-lookup"><span data-stu-id="0ef77-239">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="0ef77-240">Los clientes preguntarán por esta dirección mediante ese servicio de detección.</span><span class="sxs-lookup"><span data-stu-id="0ef77-240">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="0ef77-241">La dirección en la que los clientes obtienen tiene que tener la dirección IP o FQDN real del nodo para poder conectar.</span><span class="sxs-lookup"><span data-stu-id="0ef77-241">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="0ef77-242">Por lo que necesitará reemplazar '+' por la IP o el FQDN del nodo, como se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-242">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="0ef77-243">El último paso es agregar la lógica de procesamiento al servicio, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ef77-243">The last step is to add the processing logic to the service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="0ef77-244">`ProcessInternalRequest` lee los valores del parámetro de cadena de consulta usado para llamar a la partición y llama a `AddUserAsync` para agregar el apellido al diccionario confiable `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="0ef77-244">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="0ef77-245">Vamos a agregar un servicio sin estado al proyecto para ver cómo se puede llamar a una partición determinada.</span><span class="sxs-lookup"><span data-stu-id="0ef77-245">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="0ef77-246">Este servicio actúa como una interfaz web simple que acepta el apellido como parámetro de cadena de consulta, determina la clave de partición y la envía al servicio Alphabet.Processing para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0ef77-246">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="0ef77-247">En el cuadro de diálogo **Crear un servicio**, elija el servicio **Sin estado** y llámelo Alphabet.Web, tal y como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ef77-247">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Captura de pantalla de servicio sin estado](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="0ef77-249">.</span><span class="sxs-lookup"><span data-stu-id="0ef77-249">.</span></span>
12. <span data-ttu-id="0ef77-250">Actualice la información del punto de conexión en el archivo ServiceManifest.xml del servicio Alphabet.WebApi para abrir un puerto, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0ef77-250">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="0ef77-251">Debe devolver una colección de ServiceInstanceListeners en la clase Web.</span><span class="sxs-lookup"><span data-stu-id="0ef77-251">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="0ef77-252">De nuevo, puede elegir implementar un HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="0ef77-252">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="0ef77-253">Ahora debe implementar la lógica de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0ef77-253">Now you need to implement the processing logic.</span></span> <span data-ttu-id="0ef77-254">HttpCommunicationListener llama a `ProcessInputRequest` cuando llega una solicitud.</span><span class="sxs-lookup"><span data-stu-id="0ef77-254">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="0ef77-255">Vamos a seguir y agregar el código siguiente</span><span class="sxs-lookup"><span data-stu-id="0ef77-255">So let's go ahead and add the code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="0ef77-256">Le guiaremos paso a paso.</span><span class="sxs-lookup"><span data-stu-id="0ef77-256">Let's walk through it step by step.</span></span> <span data-ttu-id="0ef77-257">El código lee la primera letra del parámetro de la cadena de consulta `lastname` en un carácter.</span><span class="sxs-lookup"><span data-stu-id="0ef77-257">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="0ef77-258">Después determina la clave de partición de esta letra al restar el valor hexadecimal de `A` del valor hexadecimal de la primera letra de los apellidos.</span><span class="sxs-lookup"><span data-stu-id="0ef77-258">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="0ef77-259">Recuerde que, en este ejemplo, usamos 26 particiones con una clave de partición por partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-259">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="0ef77-260">A continuación, obtenemos la partición de servicio `partition` para esta clave usando el método `ResolveAsync` en el objeto `servicePartitionResolver`.</span><span class="sxs-lookup"><span data-stu-id="0ef77-260">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="0ef77-261">`servicePartitionResolver` se define como</span><span class="sxs-lookup"><span data-stu-id="0ef77-261">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="0ef77-262">El método `ResolveAsync` toma el URI del servicio, la clave de partición y un token de cancelación como parámetros.</span><span class="sxs-lookup"><span data-stu-id="0ef77-262">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="0ef77-263">El servicio de URI para el servicio de procesamiento es `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="0ef77-263">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="0ef77-264">A continuación, obtenemos el punto de conexión de la partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-264">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="0ef77-265">Por último, compilamos la dirección URL del punto de conexión además de la cadena de consulta, y llamamos al servicio de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="0ef77-265">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="0ef77-266">Después de realizar el procesamiento, escribimos la salida.</span><span class="sxs-lookup"><span data-stu-id="0ef77-266">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="0ef77-267">El último paso es probar el servicio.</span><span class="sxs-lookup"><span data-stu-id="0ef77-267">The last step is to test the service.</span></span> <span data-ttu-id="0ef77-268">Visual Studio usa parámetros de aplicación para la implementación local y de nube.</span><span class="sxs-lookup"><span data-stu-id="0ef77-268">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="0ef77-269">Para probar localmente el servicio con 26 particiones, tiene que actualizar el archivo `Local.xml` en la carpeta ApplicationParameters del proyecto AlphabetPartitions, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0ef77-269">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="0ef77-270">Cuando haya terminado la implementación, puede comprobar el servicio y todas sus particiones en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ef77-270">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![Captura de pantalla del Explorador de Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="0ef77-272">En un explorador, escriba `http://localhost:8081/?lastname=somename`probar la lógica de partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-272">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="0ef77-273">Verá que todos los apellidos que empiezan por la misma letra se almacenan en la misma partición.</span><span class="sxs-lookup"><span data-stu-id="0ef77-273">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![Captura de pantalla de explorador](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="0ef77-275">Todo el código fuente del ejemplo está disponible en [Github](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="0ef77-275">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ef77-276">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ef77-276">Next steps</span></span>
<span data-ttu-id="0ef77-277">Para obtener información sobre los conceptos de Service Fabric, vea lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ef77-277">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="0ef77-278">Disponibilidad de los servicios de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ef77-278">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="0ef77-279">Escalabilidad de servicios de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ef77-279">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="0ef77-280">Planeación de la capacidad para las aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ef77-280">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png