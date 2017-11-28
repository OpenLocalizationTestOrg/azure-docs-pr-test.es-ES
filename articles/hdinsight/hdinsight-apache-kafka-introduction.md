---
title: "aaaAn Introducción tooApache Kafka en HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de Apache Kafka en HDInsight: ¿qué es lo que hace y, donde toofind ejemplos y obtener la información de introducción."
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
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="97cb0-103">Introducción a Apache Kafka en HDInsight (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="97cb0-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="97cb0-104">[Apache Kafka](https://kafka.apache.org) es una plataforma de transmisión por secuencias distribuida de código abierto que puede ser utilizado toobuild en tiempo real de streaming las canalizaciones de datos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="97cb0-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="97cb0-105">Kafka también proporciona funcionalidad similar tooa cola de mensajes, donde puede publicar y suscribir los flujos de datos de toonamed de agente de mensajes.</span><span class="sxs-lookup"><span data-stu-id="97cb0-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="97cb0-106">Kafka en HDInsight proporciona un servicio administrado, altamente escalable y de alta disponibilidad en la nube de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="97cb0-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="97cb0-107">¿Por qué usar Kafka en HDInsight?</span><span class="sxs-lookup"><span data-stu-id="97cb0-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="97cb0-108">Kafka proporciona Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="97cb0-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="97cb0-109">Patrón de mensajería de publicación y suscripción: Kafka proporciona una API de productor para publicar registros tooa tema Kafka.</span><span class="sxs-lookup"><span data-stu-id="97cb0-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="97cb0-110">Hola consumidor API se usa cuando se suscriba tooa tema.</span><span class="sxs-lookup"><span data-stu-id="97cb0-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="97cb0-111">Procesamiento de transmisiones: Kafka se suele utilizar con Apache Storm o Spark para el procesamiento de transmisiones en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="97cb0-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="97cb0-112">Kafka 0.10.0.0 (HDInsight versión 3.5) introdujo una API de transmisión por secuencias que permite toobuild streaming soluciones sin necesidad de tormenta o Spark.</span><span class="sxs-lookup"><span data-stu-id="97cb0-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="97cb0-113">Escala horizontal: Kafka particiona secuencias en nodos de hello en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="97cb0-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="97cb0-114">Los procesos del consumidor pueden asociarse con particiones individuales tooprovide equilibrio de carga al consumir los registros.</span><span class="sxs-lookup"><span data-stu-id="97cb0-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="97cb0-115">Entrega en orden: dentro de cada partición, los registros se almacenan en la secuencia de hello en orden de Hola que se recibieron.</span><span class="sxs-lookup"><span data-stu-id="97cb0-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="97cb0-116">Al asociar un proceso de consumidor por partición, puede garantizar que los registros se procesan en orden.</span><span class="sxs-lookup"><span data-stu-id="97cb0-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="97cb0-117">Tolerancia: Las particiones se pueden replicar entre tolerancia a errores tooprovide nodos.</span><span class="sxs-lookup"><span data-stu-id="97cb0-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="97cb0-118">Integración con discos de Azure administrados: discos administrado proporciona mayor escala y rendimiento para los discos de hello utilizados por máquinas virtuales de hello en clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="97cb0-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="97cb0-119">Discos administrados están habilitados de forma predeterminada para Kafka en HDInsight y número de Hola de discos que se utilizan por nodo se puede configurar durante la creación de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97cb0-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="97cb0-120">Para más información acerca de los discos administrados, consulte [Introducción a Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97cb0-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="97cb0-121">Para obtener información acerca de la configuración de discos administrados con Kafka en HDInsight, consulte [Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Configuración del almacenamiento y la escalabilidad de Apache Kafka en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="97cb0-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="97cb0-122">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="97cb0-122">Use cases</span></span>

* <span data-ttu-id="97cb0-123">**Mensajería**: ya que admite Hola patrón de mensaje de publicación y suscripción, Kafka a menudo se utiliza como un agente de mensajes.</span><span class="sxs-lookup"><span data-stu-id="97cb0-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="97cb0-124">**Seguimiento de actividad**: Kafka ya que proporciona un registro en el orden de registros, se puede tootrack usado y volver a crear las actividades.</span><span class="sxs-lookup"><span data-stu-id="97cb0-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="97cb0-125">Por ejemplo, las acciones del usuario en un sitio web o dentro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="97cb0-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="97cb0-126">**Agregación**: mediante el procesamiento de la secuencia, puede agregar información de distintas secuencias toocombine y centralizar la información de hello en los datos operativos.</span><span class="sxs-lookup"><span data-stu-id="97cb0-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="97cb0-127">**Transformación**: mediante el procesamiento de las transmisiones, puede combinar y enriquecer los datos de varios temas de entrada en uno o más temas de salida.</span><span class="sxs-lookup"><span data-stu-id="97cb0-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97cb0-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97cb0-128">Next steps</span></span>

<span data-ttu-id="97cb0-129">Siguientes de Hola de uso vínculos toolearn cómo toouse Kafka Apache en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="97cb0-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="97cb0-130">Introducción a Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cb0-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="97cb0-131">Usar MirrorMaker toocreate una réplica de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cb0-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="97cb0-132">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cb0-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="97cb0-133">Uso de Apache Spark con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="97cb0-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="97cb0-134">Conectar tooKafka a través de una red Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="97cb0-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
