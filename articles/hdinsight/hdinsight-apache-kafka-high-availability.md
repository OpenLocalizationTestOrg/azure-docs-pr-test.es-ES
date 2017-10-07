---
title: disponibilidad de aaaHigh con Apache Kafka - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooensure alta disponibilidad con Apache Kafka en HDInsight de Azure. Obtenga información acerca de cómo toorebalance divida las réplicas en Kafka de forma que están en distintos dominios de error dentro de hello región de Azure que contiene HDInsight."
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
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="161f8-104">Alta disponibilidad de los datos con Apache Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="161f8-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="161f8-105">Obtenga información acerca de cómo tooconfigure réplicas de la partición para lograr una ventaja tootake Kafka temas del hardware subyacente bastidor configuración.</span><span class="sxs-lookup"><span data-stu-id="161f8-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="161f8-106">Esta configuración garantiza la disponibilidad de Hola de los datos almacenados en Apache Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="161f8-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="161f8-107">Dominios de error y de actualización con Kafka</span><span class="sxs-lookup"><span data-stu-id="161f8-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="161f8-108">Un dominio de error es una agrupación lógica del hardware subyacente en un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="161f8-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="161f8-109">Todos los dominios de error comparten la fuente de energía y el conmutador de red.</span><span class="sxs-lookup"><span data-stu-id="161f8-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="161f8-110">Hola las máquinas virtuales y discos administrados que implementan los nodos de hello dentro de un clúster de HDInsight se distribuyen a través de estos dominios de error.</span><span class="sxs-lookup"><span data-stu-id="161f8-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="161f8-111">Esta arquitectura limita el impacto potencial de Hola de errores de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="161f8-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="161f8-112">Cada región de Azure tiene un número concreto de dominios de error.</span><span class="sxs-lookup"><span data-stu-id="161f8-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="161f8-113">Para obtener una lista de dominios y número de Hola de dominios de error que contienen, vea hello [conjuntos de disponibilidad](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentación.</span><span class="sxs-lookup"><span data-stu-id="161f8-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="161f8-114">Kafka no es compatible con dominios de error.</span><span class="sxs-lookup"><span data-stu-id="161f8-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="161f8-115">Cuando se crea un tema en Kafka, pueden almacenar todas las réplicas de la partición en hello mismo dominio de error.</span><span class="sxs-lookup"><span data-stu-id="161f8-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="161f8-116">toosolve este problema, proporcionamos hello [herramienta equilibra particiones que Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="161f8-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="161f8-117">Cuando toorebalance partición réplicas</span><span class="sxs-lookup"><span data-stu-id="161f8-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="161f8-118">tooensure Hola mayor disponibilidad de los datos Kafka, deben reequilibrar réplicas de la partición de hello para el tema en hello siguientes veces:</span><span class="sxs-lookup"><span data-stu-id="161f8-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="161f8-119">Cuando se crean un nuevo tema o una partición</span><span class="sxs-lookup"><span data-stu-id="161f8-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="161f8-120">Cuando un clúster se escala verticalmente</span><span class="sxs-lookup"><span data-stu-id="161f8-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="161f8-121">Factor de replicación</span><span class="sxs-lookup"><span data-stu-id="161f8-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="161f8-122">Se recomienda utilizar una región de Azure que contenga tres dominios de error y un factor de replicación de 3.</span><span class="sxs-lookup"><span data-stu-id="161f8-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="161f8-123">Si debe usar una región que contiene solo dos dominios de error, use un factor de replicación de 4 réplicas de hello toospread uniformemente entre dos dominios de error Hola.</span><span class="sxs-lookup"><span data-stu-id="161f8-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="161f8-124">Para obtener un ejemplo de creación de temas y el factor de replicación de configuración hello, vea hello [iniciar con Kafka en HDInsight](hdinsight-apache-kafka-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="161f8-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="161f8-125">Cómo toorebalance particionar las réplicas</span><span class="sxs-lookup"><span data-stu-id="161f8-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="161f8-126">Hola de uso [herramienta equilibra particiones que Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance seleccionado temas.</span><span class="sxs-lookup"><span data-stu-id="161f8-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="161f8-127">Esta herramienta debe ejecutarse desde un nodo principal de SSH sesión toohello del clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="161f8-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="161f8-128">Para obtener más información sobre cómo conectar tooHDInsight mediante SSH, consulte el [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="161f8-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="161f8-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="161f8-129">Next steps</span></span>

* [<span data-ttu-id="161f8-130">Escalabilidad de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="161f8-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="161f8-131">Creación de reflejos con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="161f8-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)