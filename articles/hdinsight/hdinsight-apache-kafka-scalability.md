---
title: aaaApache Kafka aumentar escala - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure administra los discos de clúster de Apache Kafka acerca de la escalabilidad de tooincrease de HDInsight de Azure."
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Configuración del almacenamiento y la escalabilidad de Apache Kafka en HDInsight

Obtenga información acerca de cómo se utilizará el número de Hola de tooconfigure de discos administrados por Apache Kafka en HDInsight.

Kafka en HDInsight utiliza disco local de Hola de hello las máquinas virtuales en clúster de HDInsight Hola. Puesto que Kafka es E/S muy pesada, [discos de Azure administrados](../virtual-machines/windows/managed-disks-overview.md) es tooprovide usado alto rendimiento y proporcionar más espacio de almacenamiento por nodo. Si tradicionales unidades de disco duro virtuales (VHD) se utilizaron para Kafka, cada nodo es limitado too1 TB. Con los discos administrados, puede usar varios tooachieve discos 16 TB para cada nodo de clúster de Hola.

Hello diagrama siguiente proporciona una comparación entre Kafka en HDInsight antes de discos administrados y Kafka en HDInsight con discos administrados:

![Diagrama que muestra a Kafka en HDInsight con un solo disco duro virtual por cada máquina virtual frente al uso de varios discos administrados por máquina virtual](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Configuración de Managed Disks: Azure Portal

1. Siga los pasos de Hola Hola [crear un clúster de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand Hola comunes pasos toocreate un clúster mediante el portal de Hola. No se completó el proceso de creación del portal de Hola.

2. De hello __tamaño de clúster__ hoja, use hello __discos por nodo de trabajo__ tooconfigure Hola número de discos de campo.

    > [!NOTE]
    > Hello tipo de disco administrado puede ser __estándar__ (HDD) o __Premium__ (SSD). Los discos Premium se utilizan con máquinas virtuales de las series DS y GS. Todos los otros tipos de máquina virtual usan discos estándar.

    ![Imagen de hoja de tamaño de clúster de hello con discos de Hola por nodo de trabajo resaltado](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Configuración de Managed Disks: Plantilla de Resource Manager

número de hello toocontrol de discos usados por los nodos de trabajador de hello en un clúster de Kafka, Hola uso pasos de la sección de plantilla de hello:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Puede encontrar una plantilla completa que muestra cómo tooconfigure administra discos en [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo trabajar con Kafka en HDInsight, vea Hola siguientes documentos:

* [Usar MirrorMaker toocreate una réplica de Kafka en HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Uso de Apache Kafka con Storm en HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Uso de Apache Spark con Kafka en HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Conectar tooKafka a través de una red Virtual de Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Blog de HDInsight en Managed Disks con Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)