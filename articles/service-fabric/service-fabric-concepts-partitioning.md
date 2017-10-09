---
title: Servicios de Service Fabric aaaPartitioning | Documentos de Microsoft
description: "Describe cómo servicios con estado de toopartition Service Fabric. Las particiones permite el almacenamiento de datos en equipos locales de Hola para que datos y el cálculo pueden escalarse juntas."
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
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="d7500-104">Partición de Reliable Services de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7500-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="d7500-105">Este artículo proporciona una introducción toohello conceptos básicos de creación de particiones de servicios de Azure Service Fabric confiables.</span><span class="sxs-lookup"><span data-stu-id="d7500-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="d7500-106">Hello código fuente utilizada en el artículo hello también está disponible en [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="d7500-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="d7500-107">Creación de particiones</span><span class="sxs-lookup"><span data-stu-id="d7500-107">Partitioning</span></span>
<span data-ttu-id="d7500-108">La partición no es único tooService tejido.</span><span class="sxs-lookup"><span data-stu-id="d7500-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="d7500-109">De hecho, es una función básica de la compilación de servicios escalables.</span><span class="sxs-lookup"><span data-stu-id="d7500-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="d7500-110">En un sentido más amplio, podemos pensar acerca de la partición como un concepto de dividir el estado (datos) y de proceso en el rendimiento y la escalabilidad de tooimprove accesible unidades más pequeña.</span><span class="sxs-lookup"><span data-stu-id="d7500-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="d7500-111">Una forma conocida de partición es la [partición de datos][wikipartition] también conocida como particionamiento.</span><span class="sxs-lookup"><span data-stu-id="d7500-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="d7500-112">Partición de los servicios sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7500-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="d7500-113">Para los servicios sin estado, puede pensar en una partición como en una unidad lógica que contiene una o varias instancias de un servicio.</span><span class="sxs-lookup"><span data-stu-id="d7500-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="d7500-114">La ilustración 1 muestra un servicio sin estado con cinco instancias distribuidas en un clúster con una partición.</span><span class="sxs-lookup"><span data-stu-id="d7500-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Servicio sin estado](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="d7500-116">En realidad hay dos tipos de soluciones de servicios sin estado.</span><span class="sxs-lookup"><span data-stu-id="d7500-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="d7500-117">Hello primero uno es un servicio que conserva su estado externamente, por ejemplo en una base de datos de SQL Azure (por ejemplo, un sitio Web que almacena la información de sesión de Hola y de datos).</span><span class="sxs-lookup"><span data-stu-id="d7500-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="d7500-118">Hello segunda es servicios solo de cálculo (por ejemplo, una miniatura calculadora o imagen) que no se administran cualquier estado persistente.</span><span class="sxs-lookup"><span data-stu-id="d7500-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="d7500-119">En cualquier caso, la partición de un servicio sin estado es un escenarios muy poco frecuente en el que la escalabilidad y la disponibilidad normalmente se consiguen agregando más instancias.</span><span class="sxs-lookup"><span data-stu-id="d7500-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="d7500-120">las solicitudes de tiempo única de Hola que desea tooconsider varias particiones para las instancias de servicio sin estado es cuando se necesita toomeet especial enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="d7500-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="d7500-121">Por ejemplo, piense en un caso en el que los usuarios con identificadores dentro de un intervalo específico deberán ser atendidos únicamente por una instancia de servicio determinada.</span><span class="sxs-lookup"><span data-stu-id="d7500-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="d7500-122">Otro ejemplo de cuándo puede dividir un servicio sin estado es cuando tiene un backend realmente con particiones (por ejemplo, una base de datos SQL particionada) y desea toocontrol qué instancia de servicio debe escribir la partición de la base de datos de toohello--o realizar otro trabajo de preparación en Hello servicio sin estado que requiere Hola misma partición información tal como se utiliza en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="d7500-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="d7500-123">Estos tipos de escenarios también se pueden resolver de maneras diferentes y no requieren necesariamente el particionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="d7500-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="d7500-124">Hola resto de este tutorial se centra en los servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="d7500-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="d7500-125">Partición de los servicios con estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7500-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="d7500-126">Service Fabric resulta fácil toodevelop servicios con estado escalables, ya que ofrece una manera de primera clase toopartition estado (datos).</span><span class="sxs-lookup"><span data-stu-id="d7500-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="d7500-127">Conceptualmente, puede pensar en una partición de un servicio con estado como una unidad de escala es altamente confiable a través de [réplicas](service-fabric-availability-services.md) que se distribuyen y están equilibrados en los nodos de hello en un clúster.</span><span class="sxs-lookup"><span data-stu-id="d7500-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="d7500-128">Creación de particiones en el contexto de hello de servicios con estado de Service Fabric hace referencia toohello proceso de determinar que una partición de servicio en particular es responsable de una parte de todo el estado del servicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="d7500-129">(Como se mencionó anteriormente, una partición es un conjunto de [réplicas](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="d7500-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="d7500-130">Una gran ventaja de Service Fabric es que vuelve a realizar particiones de hello en nodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d7500-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="d7500-131">Esto les permite límite de recursos del nodo de toogrow tooa.</span><span class="sxs-lookup"><span data-stu-id="d7500-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="d7500-132">Como datos de hello crezca, particiones crecen y Service Fabric vuelve a equilibrar las particiones entre nodos.</span><span class="sxs-lookup"><span data-stu-id="d7500-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="d7500-133">Esto garantiza Hola sigue un uso eficaz de los recursos de hardware.</span><span class="sxs-lookup"><span data-stu-id="d7500-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="d7500-134">toogive, por ejemplo, suponga empiezan por un clúster de 5 nodos y un servicio que esté configurado toohave 10 particiones y un destino de tres réplicas.</span><span class="sxs-lookup"><span data-stu-id="d7500-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="d7500-135">En este caso, Service Fabric debería equilibrar y distribuir las réplicas de hello en el clúster de hello--y acabarías con dos principal [réplicas](service-fabric-availability-services.md) por nodo.</span><span class="sxs-lookup"><span data-stu-id="d7500-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="d7500-136">Si necesita ahora tooscale out too10 nodos del clúster de hello, Service Fabric haría reequilibrar Hola principal [réplicas](service-fabric-availability-services.md) en todos los nodos de 10.</span><span class="sxs-lookup"><span data-stu-id="d7500-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="d7500-137">Del mismo modo, si ajusta el tamaño de nodos too5 atrás, Service Fabric haría reequilibrar todas las réplicas de hello en todos los nodos de hello 5.</span><span class="sxs-lookup"><span data-stu-id="d7500-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="d7500-138">Figura 2 muestra la distribución de Hola de 10 particiones antes y después del ajuste de escala en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Servicio con estado](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="d7500-140">Como resultado, se consigue Hola escalabilidad desde las solicitudes de los clientes se distribuyen en varios equipos, se mejora el rendimiento general de la aplicación hello y se reduce la contención de toochunks de acceso de datos.</span><span class="sxs-lookup"><span data-stu-id="d7500-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="d7500-141">Plan para la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="d7500-141">Plan for partitioning</span></span>
<span data-ttu-id="d7500-142">Antes de implementar un servicio, debe considerar siempre Hola estrategia que sea necesario tooscale fuera de partición. Hay diferentes maneras, pero todos ellos se centran en la aplicación hello necesita tooachieve.</span><span class="sxs-lookup"><span data-stu-id="d7500-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="d7500-143">Para el contexto de Hola de este artículo, veamos algunos de hello aspectos más importantes.</span><span class="sxs-lookup"><span data-stu-id="d7500-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="d7500-144">Un buen enfoque es toothink acerca de la estructura de hello del estado de Hola que necesita toobe particiones, como primer paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="d7500-145">Veamos un sencillo ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d7500-145">Let's take a simple example.</span></span> <span data-ttu-id="d7500-146">Si fuera un servicio para un sondeo countywide toobuild, podría crear una partición para cada ciudad de condado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="d7500-147">A continuación, podría almacenar Hola votos para todas las personas en Ciudad hello en partición de hello correspondiente toothat ciudad.</span><span class="sxs-lookup"><span data-stu-id="d7500-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="d7500-148">Figura 3 muestra un conjunto de ciudad hello y personas en las que residen.</span><span class="sxs-lookup"><span data-stu-id="d7500-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Partición simple](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="d7500-150">Como el rellenado de Hola de ciudades varía en gran medida, puede acabar con algunas particiones que contienen una gran cantidad de datos (p. ej., Seattle) y otras particiones con muy poco estado (p. ej., Kirkland).</span><span class="sxs-lookup"><span data-stu-id="d7500-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="d7500-151">¿Cuál es el impacto de Hola de tener particiones con cantidades desiguales de estado?</span><span class="sxs-lookup"><span data-stu-id="d7500-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="d7500-152">Si piensa volver a hello (ejemplo), puede ver fácilmente que la partición de Hola que contiene Hola los votos de Seattle obtendrá más tráfico que Kirkland Hola uno.</span><span class="sxs-lookup"><span data-stu-id="d7500-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="d7500-153">De forma predeterminada, Service Fabric se asegura de que hay sobre Hola mismo número de réplicas principales y secundarias en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="d7500-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="d7500-154">Por lo que puede encontrarse con nodos que contienen réplicas que atienden más tráfico y otros que atienden de menos tráfico.</span><span class="sxs-lookup"><span data-stu-id="d7500-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="d7500-155">Preferiblemente desearía tooavoid activa y las zonas frío similar a éste en un clúster.</span><span class="sxs-lookup"><span data-stu-id="d7500-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="d7500-156">En orden tooavoid esto, debe hacer dos cosas, desde un punto de vista partición:</span><span class="sxs-lookup"><span data-stu-id="d7500-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="d7500-157">Pruebe a estado de hello toopartition para que se distribuyen uniformemente en todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="d7500-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="d7500-158">Carga de informes de cada una de las réplicas de hello para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="d7500-159">(Para más información al respecto, consulte este artículo sobre [métricas y carga](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="d7500-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="d7500-160">Service Fabric proporciona carga tooreport Hola capacidad que consumen los servicios, como la cantidad de memoria o el número de registros de.</span><span class="sxs-lookup"><span data-stu-id="d7500-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="d7500-161">Según las métricas de hello notificadas, Service Fabric detecta los que algunas particiones trabajan cargas mayores que otros y vuelve a equilibrar clúster Hola móvil réplicas toomore adecuado nodos, por lo que en general no está sobrecargado ningún nodo.</span><span class="sxs-lookup"><span data-stu-id="d7500-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="d7500-162">A veces, no es posible saber la cantidad de datos que habrá en una partición determinada.</span><span class="sxs-lookup"><span data-stu-id="d7500-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="d7500-163">Por lo que una recomendación general es toodo ambos: en primer lugar, mediante el uso de una estrategia de particiones Reparta los Hola datos uniformemente entre las particiones de hello y, después, por carga informes.</span><span class="sxs-lookup"><span data-stu-id="d7500-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="d7500-164">primer método de Hello evita situaciones descritas en hello votos de ejemplo, hello en segundo lugar contribuye a suavizar las diferencias temporales en access o carga con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="d7500-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="d7500-165">Otro aspecto de la planeación de la partición es el número correcto de hello toochoose de toobegin de particiones con.</span><span class="sxs-lookup"><span data-stu-id="d7500-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="d7500-166">Desde la perspectiva de Service Fabric, nada le impide comenzar con un número de particiones mayor del previsto para su escenario.</span><span class="sxs-lookup"><span data-stu-id="d7500-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="d7500-167">De hecho, suponiendo que el número máximo de Hola de particiones es un enfoque válido.</span><span class="sxs-lookup"><span data-stu-id="d7500-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="d7500-168">En raras ocasiones puede acabar necesitando más particiones que las elegidas inicialmente.</span><span class="sxs-lookup"><span data-stu-id="d7500-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="d7500-169">Como no se puede cambiar el recuento de particiones de hello después hechos hello, necesitaría tooapply algunos enfoques de partición avanzadas, como la creación de una nueva instancia de servicio del programa Hola a mismo tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="d7500-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="d7500-170">También necesitaría tooimplement alguna lógica de cliente que enruta Hola solicita toohello: instancia de servicio correcto, según el conocimiento de cliente que debe mantener el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="d7500-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="d7500-171">Otra consideración de planificación de la creación de particiones es recursos de los equipos disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="d7500-172">Como estado de hello debe toobe al acceso y almacenamiento, son toofollow dependiente:</span><span class="sxs-lookup"><span data-stu-id="d7500-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="d7500-173">Límites del ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="d7500-173">Network bandwidth limits</span></span>
* <span data-ttu-id="d7500-174">Límites de la memoria del sistema</span><span class="sxs-lookup"><span data-stu-id="d7500-174">System memory limits</span></span>
* <span data-ttu-id="d7500-175">Límites del almacenamiento en disco</span><span class="sxs-lookup"><span data-stu-id="d7500-175">Disk storage limits</span></span>

<span data-ttu-id="d7500-176">Por lo tanto, ¿qué ocurre si se ejecuta en las restricciones de recursos en un clúster de ejecución? respuesta de Hello es que simplemente puede escalar horizontalmente nuevos requisitos de hello clúster tooaccommodate Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="d7500-177">[Guía de planificación de capacidad de Hello](service-fabric-capacity-planning.md) se ofrecen consejos sobre cómo toodetermine cuántos nodos que necesita el clúster.</span><span class="sxs-lookup"><span data-stu-id="d7500-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="d7500-178">Introducción a la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="d7500-178">Get started with partitioning</span></span>
<span data-ttu-id="d7500-179">Esta sección describe cómo tooget a trabajar con el servicio de creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="d7500-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="d7500-180">En primer lugar, Service Fabric ofrece tres esquemas de partición posibles:</span><span class="sxs-lookup"><span data-stu-id="d7500-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="d7500-181">Particiones de intervalo (también conocidas como UniformInt64Partition)</span><span class="sxs-lookup"><span data-stu-id="d7500-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="d7500-182">Particiones con nombre.</span><span class="sxs-lookup"><span data-stu-id="d7500-182">Named partitioning.</span></span> <span data-ttu-id="d7500-183">Las aplicaciones que usan este modelo suelen tener datos que se pueden incluir en cubos, dentro de un conjunto enlazado.</span><span class="sxs-lookup"><span data-stu-id="d7500-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="d7500-184">Algunos ejemplos habituales de campos de datos que se usan como claves de partición con nombre son regiones, códigos postales, grupos de clientes u otros límites empresariales.</span><span class="sxs-lookup"><span data-stu-id="d7500-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="d7500-185">Particiones de singleton.</span><span class="sxs-lookup"><span data-stu-id="d7500-185">Singleton partitioning.</span></span> <span data-ttu-id="d7500-186">Particiones de singleton se usan normalmente cuando el servicio de hello no requiere ningún enrutamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="d7500-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="d7500-187">Por ejemplo, los servicios sin estado usan este esquema de partición de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d7500-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="d7500-188">Los esquemas de particiones con nombre y de singleton son formas especiales de particiones de intervalos.</span><span class="sxs-lookup"><span data-stu-id="d7500-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="d7500-189">De forma predeterminada, plantillas de Visual Studio de Hola para su uso de Service Fabric un rango particiones, ya que es Hola uno más habitual y útil.</span><span class="sxs-lookup"><span data-stu-id="d7500-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="d7500-190">resto de Hola de este artículo se centra en el esquema de partición rango Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="d7500-191">Esquema de particiones de intervalo</span><span class="sxs-lookup"><span data-stu-id="d7500-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="d7500-192">Se trata de toospecify usa un entero intervalo (identificadas mediante una clave baja y clave superior) y un número de particiones (n).</span><span class="sxs-lookup"><span data-stu-id="d7500-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="d7500-193">Crea particiones de n, uno de ellos responsables un subintervalo no superpuestos de hello general rangos con clave de partición.</span><span class="sxs-lookup"><span data-stu-id="d7500-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="d7500-194">Por ejemplo: un esquema de partición de intervalo con una clave baja 0, una clave alta de 99 y un recuento de 4 crearía 4 particiones, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7500-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Creación de particiones por rangos](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="d7500-196">Un enfoque común es toocreate un hash basado en una clave única en el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="d7500-197">Algunos ejemplos comunes de claves son un número de identificación de vehículo (VIN), identificación de empleado o una cadena única.</span><span class="sxs-lookup"><span data-stu-id="d7500-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="d7500-198">Mediante el uso de esta clave única, a continuación, podría generar un código hash, intervalo de claves de módulo hello, toouse como su clave.</span><span class="sxs-lookup"><span data-stu-id="d7500-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="d7500-199">Puede especificar Hola superior e inferior de hello clave intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="d7500-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="d7500-200">Selección de un algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="d7500-200">Select a hash algorithm</span></span>
<span data-ttu-id="d7500-201">Una parte importante de los algoritmos hash es seleccionar su algoritmo hash.</span><span class="sxs-lookup"><span data-stu-id="d7500-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="d7500-202">Debe tener en cuenta es si el objetivo de hello toogroup claves similar cerca entre sí (hash confidencial localidad)--o si la actividad debe distribuirse ampliamente en todas las particiones (hash de distribución), lo que es más común.</span><span class="sxs-lookup"><span data-stu-id="d7500-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="d7500-203">características de Hola de un algoritmo hash de distribución óptimas son que resulta fácil toocompute, tiene algunas de las colisiones y se distribuye uniformemente las claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="d7500-204">Un buen ejemplo de un algoritmo hash eficaz es hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algoritmo hash.</span><span class="sxs-lookup"><span data-stu-id="d7500-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="d7500-205">Un buen recurso para opciones de algoritmo de código hash general es hello [página de Wikipedia en las funciones de hash](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="d7500-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="d7500-206">Creación de un servicio con estado con varias particiones</span><span class="sxs-lookup"><span data-stu-id="d7500-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="d7500-207">Vamos a crear su primer servicio con estado confiable con varias particiones.</span><span class="sxs-lookup"><span data-stu-id="d7500-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="d7500-208">En este ejemplo, va a compilar una aplicación muy simple en el que desea toostore todos los apellidos que comienzan con hello en Hola de letra misma partición.</span><span class="sxs-lookup"><span data-stu-id="d7500-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="d7500-209">Antes de escribir ningún código, debe toothink acerca de las particiones de Hola y las claves de partición.</span><span class="sxs-lookup"><span data-stu-id="d7500-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="d7500-210">Necesita 26 particiones (uno para cada letra del alfabeto hello), pero ¿qué pasa sobre Hola claves alta y bajas?</span><span class="sxs-lookup"><span data-stu-id="d7500-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="d7500-211">Puesto que queremos literalmente toohave una partición por letra, podemos usar 0 como clave baja de Hola y 25 como clave alta de hello, como cada letra es su propia clave.</span><span class="sxs-lookup"><span data-stu-id="d7500-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="d7500-212">Se trata de un escenario simplificado, ya que en realidad distribución Hola sería desigual.</span><span class="sxs-lookup"><span data-stu-id="d7500-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="d7500-213">Apellidos que empiezan con las letras de hello "S" o "M" son más comunes que Hola que empiezan por "X" o "Y".</span><span class="sxs-lookup"><span data-stu-id="d7500-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="d7500-214">Abra **Visual Studio** > **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d7500-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="d7500-215">Hola **nuevo proyecto** diálogo cuadro, seleccione la aplicación de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d7500-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="d7500-216">Llame al proyecto de Hola "AlphabetPartitions".</span><span class="sxs-lookup"><span data-stu-id="d7500-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="d7500-217">Hola **crear un servicio** diálogo cuadro, elija **Stateful** de servicio y llámelo "Alphabet.Processing" como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="d7500-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="d7500-218">![Cuadro de diálogo de servicio nuevo en Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="d7500-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="d7500-219">Establecer número de Hola de particiones.</span><span class="sxs-lookup"><span data-stu-id="d7500-219">Set hello number of partitions.</span></span> <span data-ttu-id="d7500-220">Archivo de Applicationmanifest.xml de hello abierto encuentra en hello ApplicationPackageRoot carpeta de hello AlphabetPartitions proyecto y actualice parámetro hello Processing_PartitionCount too26 tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7500-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="d7500-221">También necesitará hello tooupdate LowKey y HighKey propiedades del elemento de StatefulService Hola Hola ApplicationManifest.xml tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7500-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="d7500-222">Para el servicio de hello toobe accesible, abrir un extremo en un puerto mediante la adición de elemento de punto de conexión de Hola de ServiceManifest.xml (que se encuentra en la carpeta de PackageRoot hello) para hello Alphabet.Processing servicio tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="d7500-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="d7500-223">Ahora servicio hello es toolisten configurado tooan extremo interno con 26 particiones.</span><span class="sxs-lookup"><span data-stu-id="d7500-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="d7500-224">A continuación, debe toooverride hello `CreateServiceReplicaListeners()` método de clase de procesamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7500-225">Para este ejemplo, asumimos que está usando un HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="d7500-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="d7500-226">Para obtener más información sobre la comunicación del servicio confiable, vea [modelo de comunicación de un servicio confiable de hello](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="d7500-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="d7500-227">Un patrón recomendado para URL de Hola que escucha una réplica es hello siguiendo el formato: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="d7500-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="d7500-228">Por lo que desee tooconfigure su toolisten de agente de escucha de comunicación en los puntos de conexión correcto de Hola y con este patrón.</span><span class="sxs-lookup"><span data-stu-id="d7500-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="d7500-229">Varias réplicas de este servicio pueden estar hospedadas en hello mismo equipo, por lo que esta dirección debe toobe toohello única réplica.</span><span class="sxs-lookup"><span data-stu-id="d7500-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="d7500-230">Esta es la razón por Id. de partición + Id. de réplica en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="d7500-231">HttpListener puede escuchar en varias direcciones en hello que mismo número de puerto como prefijo de dirección URL de hello es único.</span><span class="sxs-lookup"><span data-stu-id="d7500-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="d7500-232">Hola que GUID adicional es por un caso avanzado donde las réplicas secundarias también escuchan las solicitudes de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="d7500-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="d7500-233">Una vez que el caso de hello, desea toomake seguro de que una nueva dirección única se utiliza al realizar la transición desde la dirección de toosecondary principal tooforce clientes toore resolución Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="d7500-234">'+' se utiliza como dirección de hello aquí para que hello réplica escucha en el código de hello con todos los hosts disponibles (IP, FQDM, localhost, etc.) a continuación muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d7500-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
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
   
    <span data-ttu-id="d7500-235">También merece la pena mencionar que Hola publicado direcciones URL es ligeramente diferente de prefijo de dirección URL de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="d7500-236">dirección URL de escucha de Hello tiene tooHttpListener.</span><span class="sxs-lookup"><span data-stu-id="d7500-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="d7500-237">Hola que dirección URL publicada es dirección URL de Hola que está publicada toohello tejido nomenclatura servicio, que se usa para la detección de servicios.</span><span class="sxs-lookup"><span data-stu-id="d7500-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="d7500-238">Los clientes preguntarán por esta dirección mediante ese servicio de detección.</span><span class="sxs-lookup"><span data-stu-id="d7500-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="d7500-239">dirección de Hola que los clientes tengan necesidades toohave Hola real IP o FQDN del nodo de hello en orden tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d7500-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="d7500-240">Por lo que necesita tooreplace '+' con Hola del nodo IP o FQDN tal como se muestra arriba.</span><span class="sxs-lookup"><span data-stu-id="d7500-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="d7500-241">Hola último paso es hello tooadd lógica toohello servicio tal y como se muestra a continuación de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="d7500-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
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
   
    <span data-ttu-id="d7500-242">`ProcessInternalRequest`lecturas Hola valores de hello consulta cadena parámetro utilizado toocall Hola partición y las llamadas `AddUserAsync` diccionario confiable de tooadd Hola lastname toohello `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="d7500-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="d7500-243">Vamos a agregar un toosee de proyecto de servicio sin estado toohello cómo puede llamar a una partición determinada.</span><span class="sxs-lookup"><span data-stu-id="d7500-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="d7500-244">Este servicio actúa como una sencilla interfaz web que acepta Hola lastname como un parámetro de cadena de consulta, determina la clave de partición de Hola y lo envía toohello Alphabet.Processing servicio para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="d7500-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="d7500-245">Hola **crear un servicio** diálogo cuadro, elija **Stateless** de servicio y llámelo "Alphabet.Web", tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7500-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Captura de pantalla de servicio sin estado](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="d7500-247">.</span><span class="sxs-lookup"><span data-stu-id="d7500-247">.</span></span>
12. <span data-ttu-id="d7500-248">Actualizar la información de punto de conexión de hello en hello ServiceManifest.xml de hello Alphabet.WebApi servicio tooopen un puerto tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d7500-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="d7500-249">Debe tooreturn una colección de ServiceInstanceListeners en la clase de hello Web.</span><span class="sxs-lookup"><span data-stu-id="d7500-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="d7500-250">De nuevo, puede elegir tooimplement un HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="d7500-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="d7500-251">Ahora necesita lógica de procesamiento de tooimplement Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="d7500-252">Hola HttpCommunicationListener llamadas `ProcessInputRequest` cuando llega una solicitud.</span><span class="sxs-lookup"><span data-stu-id="d7500-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="d7500-253">Por lo que sigamos adelante y agregar código de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="d7500-253">So let's go ahead and add hello code below.</span></span>
    
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
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
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
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="d7500-254">Le guiaremos paso a paso.</span><span class="sxs-lookup"><span data-stu-id="d7500-254">Let's walk through it step by step.</span></span> <span data-ttu-id="d7500-255">código de Hello lee la primera letra de Hola de parámetro de cadena de consulta de hello `lastname` en un valor char.</span><span class="sxs-lookup"><span data-stu-id="d7500-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="d7500-256">A continuación, determina clave de partición de Hola para esta letra restando el valor hexadecimal de Hola de `A` de valor hexadecimal de saludo de la primera letra de hello apellidos.</span><span class="sxs-lookup"><span data-stu-id="d7500-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="d7500-257">Recuerde que, en este ejemplo, usamos 26 particiones con una clave de partición por partición.</span><span class="sxs-lookup"><span data-stu-id="d7500-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="d7500-258">A continuación, obtenemos la partición de servicio de hello `partition` para esta clave mediante el uso de hello `ResolveAsync` método en hello `servicePartitionResolver` objeto.</span><span class="sxs-lookup"><span data-stu-id="d7500-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="d7500-259">`servicePartitionResolver` se define como</span><span class="sxs-lookup"><span data-stu-id="d7500-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="d7500-260">Hola `ResolveAsync` método toma Hola servicio URI, clave de partición de Hola y un token de cancelación como parámetros.</span><span class="sxs-lookup"><span data-stu-id="d7500-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="d7500-261">Hola URI del servicio de servicio de procesamiento de hello es `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="d7500-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="d7500-262">A continuación, obtenemos el punto de conexión de Hola de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="d7500-263">Por último, se compilación dirección URL del extremo de Hola y Hola querystring y llamar al servicio de procesamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7500-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="d7500-264">Una vez que se realiza el procesamiento de hello, se escribe un resultado Hola atrás.</span><span class="sxs-lookup"><span data-stu-id="d7500-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="d7500-265">Hola último paso es servicio de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="d7500-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="d7500-266">Visual Studio usa parámetros de aplicación para la implementación local y de nube.</span><span class="sxs-lookup"><span data-stu-id="d7500-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="d7500-267">servicio de hello tootest con 26 particiones localmente, necesita tooupdate hello `Local.xml` archivos en la carpeta de ApplicationParameters de hello del proyecto de hello AlphabetPartitions tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="d7500-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="d7500-268">Después de finalizar la implementación, puede comprobar el servicio de Hola y todas sus particiones de hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7500-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Captura de pantalla del Explorador de Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="d7500-270">En un explorador, puede probar Hola partición lógica escribiendo `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="d7500-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="d7500-271">Verá que cada nombre de la última que se inicia con la misma letra se esté almacenando en Hola de Hola misma partición.</span><span class="sxs-lookup"><span data-stu-id="d7500-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Captura de pantalla de explorador](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="d7500-273">Hola todo código de ejemplo de Hola está disponible en [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="d7500-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7500-274">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7500-274">Next steps</span></span>
<span data-ttu-id="d7500-275">Para obtener información sobre conceptos de Service Fabric, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7500-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="d7500-276">Disponibilidad de los servicios de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7500-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="d7500-277">Escalabilidad de servicios de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7500-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="d7500-278">Planeación de la capacidad para las aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7500-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png