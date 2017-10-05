---
title: "Introducción a Apache Kafka en Azure HDInsight | Microsoft Docs"
description: "Información sobre Apache Kafka en HDInsight: qué es, qué hace y dónde encontrar ejemplos y obtener una introducción."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1976c52bd7fa56bb07104e205ab3699b2dfa4c50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="5b699-103">Introducción a Apache Kafka en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="5b699-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="5b699-104">[Apache Kafka](https://kafka.apache.org) es una plataforma de streaming distribuido de código abierto que se puede utilizar para compilar canalizaciones de datos de streaming en tiempo real y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5b699-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="5b699-105">Kafka también proporciona funcionalidad de agente de mensajería similar a una cola de mensajes, donde puede publicar y suscribirse a las transmisiones de datos con nombre.</span><span class="sxs-lookup"><span data-stu-id="5b699-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="5b699-106">Kafka en HDInsight proporciona un servicio administrado, altamente escalable y de alta disponibilidad en la nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5b699-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="5b699-107">¿Por qué usar Kafka en HDInsight?</span><span class="sxs-lookup"><span data-stu-id="5b699-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="5b699-108">Kafka ofrece las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="5b699-108">Kafka provides the following features:</span></span>

* <span data-ttu-id="5b699-109">Patrón de mensajería de publicación y suscripción: Kafka proporciona una API de productor para publicar registros a un tema de Kafka.</span><span class="sxs-lookup"><span data-stu-id="5b699-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="5b699-110">Al suscribirse a un tema, se utiliza la API de consumidor.</span><span class="sxs-lookup"><span data-stu-id="5b699-110">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="5b699-111">Procesamiento de transmisiones: Kafka se suele utilizar con Apache Storm o Spark para el procesamiento de transmisiones en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="5b699-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="5b699-112">Kafka 0.10.0.0 (HDInsight versión 3.5) introdujo una API de streaming que permite generar soluciones de streaming sin necesidad de Storm ni Spark.</span><span class="sxs-lookup"><span data-stu-id="5b699-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="5b699-113">Escala horizontal: Kafka particiona las transmisiones en los nodos del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b699-113">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="5b699-114">Los procesos del consumidor se pueden asociar con las particiones individuales para proporcionar equilibrio de carga al consumir los registros.</span><span class="sxs-lookup"><span data-stu-id="5b699-114">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="5b699-115">Entrega en orden: dentro de cada partición, los registros se almacenan en la transmisión en el orden en que se recibieron.</span><span class="sxs-lookup"><span data-stu-id="5b699-115">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="5b699-116">Al asociar un proceso de consumidor por partición, puede garantizar que los registros se procesan en orden.</span><span class="sxs-lookup"><span data-stu-id="5b699-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="5b699-117">Tolerancia a errores: las particiones pueden replicarse entre los nodos para proporcionar tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="5b699-117">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

* <span data-ttu-id="5b699-118">Integración con Azure Managed Disks: Managed Disks proporciona mayor escala y rendimiento a los discos que usan las máquinas virtuales en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b699-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for the disks used by the virtual machines in the HDInsight cluster.</span></span>

    <span data-ttu-id="5b699-119">Los discos administrados están habilitados de forma predeterminada para Kafka en HDInsight y el número de discos que se utilizan por nodo se puede configurar durante la creación de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b699-119">Managed disks are enabled by default for Kafka on HDInsight, and the number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="5b699-120">Para más información acerca de los discos administrados, consulte [Introducción a Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b699-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="5b699-121">Para obtener información acerca de la configuración de discos administrados con Kafka en HDInsight, consulte [Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Configuración del almacenamiento y la escalabilidad de Apache Kafka en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="5b699-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="5b699-122">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="5b699-122">Use cases</span></span>

* <span data-ttu-id="5b699-123">**Mensajería**: como admite el patrón de publicación de mensajes y suscripción, Kafka a menudo se utiliza como agente de mensajería.</span><span class="sxs-lookup"><span data-stu-id="5b699-123">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="5b699-124">**Seguimiento de la actividad**: Kafka proporciona un registro en orden, por lo que se puede utilizar para realizar un seguimiento y volver a crear actividades.</span><span class="sxs-lookup"><span data-stu-id="5b699-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="5b699-125">Por ejemplo, las acciones del usuario en un sitio web o dentro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b699-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="5b699-126">**Agregación**: mediante el procesamiento de las transmisiones, puede agregar información de distintas transmisiones para combinar y centralizar la información en datos operativos.</span><span class="sxs-lookup"><span data-stu-id="5b699-126">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="5b699-127">**Transformación**: mediante el procesamiento de las transmisiones, puede combinar y enriquecer los datos de varios temas de entrada en uno o más temas de salida.</span><span class="sxs-lookup"><span data-stu-id="5b699-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b699-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b699-128">Next steps</span></span>

<span data-ttu-id="5b699-129">Use los vínculos siguientes para aprender a usar a Apache Kafka en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5b699-129">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="5b699-130">Introducción a Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b699-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="5b699-131">Uso de MirrorMaker para crear una réplica de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b699-131">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="5b699-132">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b699-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="5b699-133">Uso de Apache Spark con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b699-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="5b699-134">Conexión a Kafka a través de una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="5b699-134">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)