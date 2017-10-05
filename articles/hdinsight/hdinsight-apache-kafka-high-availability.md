---
title: Alta disponibilidad con Apache Kafka en Azure HDInsight | Microsoft Docs
description: "Aprenda a garantizar una alta disponibilidad con Apache Kafka en Azure HDInsight. Aprenda a reequilibrar réplicas de partición en Kafka para que se encuentren en distintos dominios de error en la región de Azure que contenga HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="e99de-104">Alta disponibilidad de los datos con Apache Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e99de-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="e99de-105">Aprenda a configurar réplicas de partición para que los temas de Kafka saquen provecho de la configuración del bastidor de hardware subyacente.</span><span class="sxs-lookup"><span data-stu-id="e99de-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="e99de-106">Esta configuración garantiza la disponibilidad de los datos almacenados en Apache Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e99de-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="e99de-107">Dominios de error y de actualización con Kafka</span><span class="sxs-lookup"><span data-stu-id="e99de-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="e99de-108">Un dominio de error es una agrupación lógica del hardware subyacente en un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e99de-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="e99de-109">Todos los dominios de error comparten la fuente de energía y el conmutador de red.</span><span class="sxs-lookup"><span data-stu-id="e99de-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="e99de-110">Las máquinas virtuales y los discos administrados que implementan los nodos en un clúster de HDInsight se distribuyen por estos dominios de error.</span><span class="sxs-lookup"><span data-stu-id="e99de-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="e99de-111">Esta arquitectura limita el impacto potencial de errores del hardware físico.</span><span class="sxs-lookup"><span data-stu-id="e99de-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="e99de-112">Cada región de Azure tiene un número concreto de dominios de error.</span><span class="sxs-lookup"><span data-stu-id="e99de-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="e99de-113">Para obtener una lista de los dominios y el número de dominios de error que contienen, consulte la documentación de los [conjuntos de disponibilidad](../virtual-machines/linux/regions-and-availability.md#availability-sets).</span><span class="sxs-lookup"><span data-stu-id="e99de-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e99de-114">Kafka no es compatible con dominios de error.</span><span class="sxs-lookup"><span data-stu-id="e99de-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="e99de-115">Cuando se crea un tema en Kafka, este puede almacenar todas las réplicas de las particiones en el mismo dominio de error.</span><span class="sxs-lookup"><span data-stu-id="e99de-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="e99de-116">Para solucionar este problema, proporcionamos la [herramienta de reequilibrio de particiones de Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="e99de-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="e99de-117">Cuándo se deben reequilibrar las réplicas de las particiones</span><span class="sxs-lookup"><span data-stu-id="e99de-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="e99de-118">Para garantizar la máxima disponibilidad de los datos de Kafka, es preciso reequilibrar las réplicas de las particiones del tema en las siguientes ocasiones:</span><span class="sxs-lookup"><span data-stu-id="e99de-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="e99de-119">Cuando se crean un nuevo tema o una partición</span><span class="sxs-lookup"><span data-stu-id="e99de-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="e99de-120">Cuando un clúster se escala verticalmente</span><span class="sxs-lookup"><span data-stu-id="e99de-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="e99de-121">Factor de replicación</span><span class="sxs-lookup"><span data-stu-id="e99de-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e99de-122">Se recomienda utilizar una región de Azure que contenga tres dominios de error y un factor de replicación de 3.</span><span class="sxs-lookup"><span data-stu-id="e99de-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="e99de-123">Si debe usar una región que contenga solo dos dominios de error, use un factor de replicación de 4 para distribuir las réplicas uniformemente entre los dominios de error de dos.</span><span class="sxs-lookup"><span data-stu-id="e99de-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="e99de-124">Para obtener un ejemplo de creación de temas y establecimiento del factor de replicación, consulte el documento [Introducción a Apache Kafka (versión preliminar) en HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e99de-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="e99de-125">Reequilibrio de réplicas de particiones</span><span class="sxs-lookup"><span data-stu-id="e99de-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="e99de-126">Use la [herramienta de reequilibrio de particiones de Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) reequilibrar los temas seleccionados.</span><span class="sxs-lookup"><span data-stu-id="e99de-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="e99de-127">Esta herramienta se debe ejecutar desde una sesión de SSH en el nodo principal del clúster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="e99de-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="e99de-128">Para más información acerca de la conexión con HDInsight mediante SSH, consulte el documento [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e99de-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e99de-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e99de-129">Next steps</span></span>

* [<span data-ttu-id="e99de-130">Escalabilidad de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e99de-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="e99de-131">Creación de reflejos con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e99de-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)