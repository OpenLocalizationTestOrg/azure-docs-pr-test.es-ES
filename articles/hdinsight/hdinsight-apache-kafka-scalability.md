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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="00892-103">Configuración del almacenamiento y la escalabilidad de Apache Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="00892-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="00892-104">Obtenga información acerca de cómo se utilizará el número de Hola de tooconfigure de discos administrados por Apache Kafka en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00892-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="00892-105">Kafka en HDInsight utiliza disco local de Hola de hello las máquinas virtuales en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="00892-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="00892-106">Puesto que Kafka es E/S muy pesada, [discos de Azure administrados](../virtual-machines/windows/managed-disks-overview.md) es tooprovide usado alto rendimiento y proporcionar más espacio de almacenamiento por nodo.</span><span class="sxs-lookup"><span data-stu-id="00892-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="00892-107">Si tradicionales unidades de disco duro virtuales (VHD) se utilizaron para Kafka, cada nodo es limitado too1 TB.</span><span class="sxs-lookup"><span data-stu-id="00892-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="00892-108">Con los discos administrados, puede usar varios tooachieve discos 16 TB para cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="00892-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="00892-109">Hello diagrama siguiente proporciona una comparación entre Kafka en HDInsight antes de discos administrados y Kafka en HDInsight con discos administrados:</span><span class="sxs-lookup"><span data-stu-id="00892-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagrama que muestra a Kafka en HDInsight con un solo disco duro virtual por cada máquina virtual frente al uso de varios discos administrados por máquina virtual](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="00892-111">Configuración de Managed Disks: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00892-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="00892-112">Siga los pasos de Hola Hola [crear un clúster de HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand Hola comunes pasos toocreate un clúster mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="00892-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="00892-113">No se completó el proceso de creación del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="00892-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="00892-114">De hello __tamaño de clúster__ hoja, use hello __discos por nodo de trabajo__ tooconfigure Hola número de discos de campo.</span><span class="sxs-lookup"><span data-stu-id="00892-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="00892-115">Hello tipo de disco administrado puede ser __estándar__ (HDD) o __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="00892-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="00892-116">Los discos Premium se utilizan con máquinas virtuales de las series DS y GS.</span><span class="sxs-lookup"><span data-stu-id="00892-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="00892-117">Todos los otros tipos de máquina virtual usan discos estándar.</span><span class="sxs-lookup"><span data-stu-id="00892-117">All other VM types use standard.</span></span>

    ![Imagen de hoja de tamaño de clúster de hello con discos de Hola por nodo de trabajo resaltado](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="00892-119">Configuración de Managed Disks: Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="00892-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="00892-120">número de hello toocontrol de discos usados por los nodos de trabajador de hello en un clúster de Kafka, Hola uso pasos de la sección de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="00892-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="00892-121">Puede encontrar una plantilla completa que muestra cómo tooconfigure administra discos en [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="00892-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00892-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00892-122">Next steps</span></span>

<span data-ttu-id="00892-123">Para obtener más información sobre cómo trabajar con Kafka en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="00892-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="00892-124">Usar MirrorMaker toocreate una réplica de Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="00892-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="00892-125">Uso de Apache Kafka con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="00892-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="00892-126">Uso de Apache Spark con Kafka en HDInsight</span><span class="sxs-lookup"><span data-stu-id="00892-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="00892-127">Conectar tooKafka a través de una red Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="00892-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="00892-128">Blog de HDInsight en Managed Disks con Kafka</span><span class="sxs-lookup"><span data-stu-id="00892-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)