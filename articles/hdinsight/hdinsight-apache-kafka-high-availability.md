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
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Alta disponibilidad de los datos con Apache Kafka (versión preliminar) en HDInsight

Obtenga información acerca de cómo tooconfigure réplicas de la partición para lograr una ventaja tootake Kafka temas del hardware subyacente bastidor configuración. Esta configuración garantiza la disponibilidad de Hola de los datos almacenados en Apache Kafka en HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Dominios de error y de actualización con Kafka

Un dominio de error es una agrupación lógica del hardware subyacente en un centro de datos de Azure. Todos los dominios de error comparten la fuente de energía y el conmutador de red. Hola las máquinas virtuales y discos administrados que implementan los nodos de hello dentro de un clúster de HDInsight se distribuyen a través de estos dominios de error. Esta arquitectura limita el impacto potencial de Hola de errores de hardware físico.

Cada región de Azure tiene un número concreto de dominios de error. Para obtener una lista de dominios y número de Hola de dominios de error que contienen, vea hello [conjuntos de disponibilidad](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentación.

> [!IMPORTANT]
> Kafka no es compatible con dominios de error. Cuando se crea un tema en Kafka, pueden almacenar todas las réplicas de la partición en hello mismo dominio de error. toosolve este problema, proporcionamos hello [herramienta equilibra particiones que Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Cuando toorebalance partición réplicas

tooensure Hola mayor disponibilidad de los datos Kafka, deben reequilibrar réplicas de la partición de hello para el tema en hello siguientes veces:

* Cuando se crean un nuevo tema o una partición

* Cuando un clúster se escala verticalmente

## <a name="replication-factor"></a>Factor de replicación

> [!IMPORTANT]
> Se recomienda utilizar una región de Azure que contenga tres dominios de error y un factor de replicación de 3.

Si debe usar una región que contiene solo dos dominios de error, use un factor de replicación de 4 réplicas de hello toospread uniformemente entre dos dominios de error Hola.

Para obtener un ejemplo de creación de temas y el factor de replicación de configuración hello, vea hello [iniciar con Kafka en HDInsight](hdinsight-apache-kafka-get-started.md) documento.

## <a name="how-toorebalance-partition-replicas"></a>Cómo toorebalance particionar las réplicas

Hola de uso [herramienta equilibra particiones que Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance seleccionado temas. Esta herramienta debe ejecutarse desde un nodo principal de SSH sesión toohello del clúster Kafka.

Para obtener más información sobre cómo conectar tooHDInsight mediante SSH, consulte el [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

## <a name="next-steps"></a>Pasos siguientes

* [Escalabilidad de Kafka en HDInsight](hdinsight-apache-kafka-scalability.md)
* [Creación de reflejos con Kafka en HDInsight](hdinsight-apache-kafka-mirroring.md)