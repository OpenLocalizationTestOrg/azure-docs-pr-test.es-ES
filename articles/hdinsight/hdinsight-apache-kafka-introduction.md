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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Introducción a Apache Kafka en HDInsight (versión preliminar)

[Apache Kafka](https://kafka.apache.org) es una plataforma de transmisión por secuencias distribuida de código abierto que puede ser utilizado toobuild en tiempo real de streaming las canalizaciones de datos y aplicaciones. Kafka también proporciona funcionalidad similar tooa cola de mensajes, donde puede publicar y suscribir los flujos de datos de toonamed de agente de mensajes. Kafka en HDInsight proporciona un servicio administrado, altamente escalable y de alta disponibilidad en la nube de Microsoft Azure Hola.

## <a name="why-use-kafka-on-hdinsight"></a>¿Por qué usar Kafka en HDInsight?

Kafka proporciona Hola siguientes características:

* Patrón de mensajería de publicación y suscripción: Kafka proporciona una API de productor para publicar registros tooa tema Kafka. Hola consumidor API se usa cuando se suscriba tooa tema.

* Procesamiento de transmisiones: Kafka se suele utilizar con Apache Storm o Spark para el procesamiento de transmisiones en tiempo real. Kafka 0.10.0.0 (HDInsight versión 3.5) introdujo una API de transmisión por secuencias que permite toobuild streaming soluciones sin necesidad de tormenta o Spark.

* Escala horizontal: Kafka particiona secuencias en nodos de hello en clúster de HDInsight Hola. Los procesos del consumidor pueden asociarse con particiones individuales tooprovide equilibrio de carga al consumir los registros.

* Entrega en orden: dentro de cada partición, los registros se almacenan en la secuencia de hello en orden de Hola que se recibieron. Al asociar un proceso de consumidor por partición, puede garantizar que los registros se procesan en orden.

* Tolerancia: Las particiones se pueden replicar entre tolerancia a errores tooprovide nodos.

* Integración con discos de Azure administrados: discos administrado proporciona mayor escala y rendimiento para los discos de hello utilizados por máquinas virtuales de hello en clúster de HDInsight de Hola.

    Discos administrados están habilitados de forma predeterminada para Kafka en HDInsight y número de Hola de discos que se utilizan por nodo se puede configurar durante la creación de HDInsight. Para más información acerca de los discos administrados, consulte [Introducción a Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).

    Para obtener información acerca de la configuración de discos administrados con Kafka en HDInsight, consulte [Configure storage and scalability for Apache Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Configuración del almacenamiento y la escalabilidad de Apache Kafka en HDInsight).

## <a name="use-cases"></a>Casos de uso

* **Mensajería**: ya que admite Hola patrón de mensaje de publicación y suscripción, Kafka a menudo se utiliza como un agente de mensajes.

* **Seguimiento de actividad**: Kafka ya que proporciona un registro en el orden de registros, se puede tootrack usado y volver a crear las actividades. Por ejemplo, las acciones del usuario en un sitio web o dentro de una aplicación.

* **Agregación**: mediante el procesamiento de la secuencia, puede agregar información de distintas secuencias toocombine y centralizar la información de hello en los datos operativos.

* **Transformación**: mediante el procesamiento de las transmisiones, puede combinar y enriquecer los datos de varios temas de entrada en uno o más temas de salida.

## <a name="next-steps"></a>Pasos siguientes

Siguientes de Hola de uso vínculos toolearn cómo toouse Kafka Apache en HDInsight:

* [Introducción a Kafka en HDInsight](hdinsight-apache-kafka-get-started.md)

* [Usar MirrorMaker toocreate una réplica de Kafka en HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Uso de Apache Kafka con Storm en HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Uso de Apache Spark con Kafka en HDInsight](hdinsight-apache-spark-with-kafka.md)

* [Conectar tooKafka a través de una red Virtual de Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
