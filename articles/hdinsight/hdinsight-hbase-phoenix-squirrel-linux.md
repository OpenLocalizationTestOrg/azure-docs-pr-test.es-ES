---
title: Uso de Apache Phoenix y SQuirreL con HBase - Azure HDInsight | Microsoft Docs
description: "Aprenda a usar Apache Phoenix en HDInsight y cómo instalar y configurar SQuirreL en su estación de trabajo para conectarse a un clúster de HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="101b1-103">Uso de Apache Phoenix con clústeres de HBase basados en Linux en HDInsight</span><span class="sxs-lookup"><span data-stu-id="101b1-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="101b1-104">Aprenda a utilizar [Apache Phoenix](http://phoenix.apache.org/) en HDInsight y SQLLine.</span><span class="sxs-lookup"><span data-stu-id="101b1-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="101b1-105">Para obtener más información acerca de Phoenix, consulte [Phoenix en 15 minutos o menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="101b1-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="101b1-106">Para la gramática de Phoenix, vea [Gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="101b1-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="101b1-107">Para obtener información de la versión de Phoenix en HDInsight, consulte [Novedades en las versiones de clústeres de Hadoop proporcionadas por HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="101b1-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="101b1-108">Uso de SQLLine</span><span class="sxs-lookup"><span data-stu-id="101b1-108">Use SQLLine</span></span>
<span data-ttu-id="101b1-109">[SQLLine](http://sqlline.sourceforge.net/) es una utilidad de línea de comandos para ejecutar SQL.</span><span class="sxs-lookup"><span data-stu-id="101b1-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="101b1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="101b1-110">Prerequisites</span></span>
<span data-ttu-id="101b1-111">Antes de usar SQLLine, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="101b1-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="101b1-112">**Un clúster de HBase en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="101b1-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="101b1-113">Para obtener información sobre el aprovisionamiento del clúster de HBase, consulte [Introducción a HBase Apache en HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="101b1-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="101b1-114">**Conexión al clúster de HBase a través del protocolo de escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="101b1-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="101b1-115">Para obtener instrucciones, vea [Administración de clústeres de Hadoop en HDInsight mediante el Portal de Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="101b1-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="101b1-116">Cuando se conecte a un clúster de HBase, deberá conectarse a uno de los Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="101b1-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="101b1-117">Cada clúster de HDInsight tiene tres Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="101b1-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="101b1-118">**Para averiguar el nombre de host de ZooKeeper**</span><span class="sxs-lookup"><span data-stu-id="101b1-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="101b1-119">Abra Ambari; para ello, vaya a **https://<ClusterName>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="101b1-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="101b1-120">Escriba el nombre de usuario HTTP (clúster) y la contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="101b1-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="101b1-121">En el menú izquierdo, haga clic en **ZooKeeper** .</span><span class="sxs-lookup"><span data-stu-id="101b1-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="101b1-122">Verá una lista con los tres **servidores de ZooKeeper**.</span><span class="sxs-lookup"><span data-stu-id="101b1-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="101b1-123">Haga clic en uno de los **servidores de ZooKeeper** que aparecen.</span><span class="sxs-lookup"><span data-stu-id="101b1-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="101b1-124">En el panel Resumen, busque el **Nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="101b1-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="101b1-125">Es similar a *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="101b1-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="101b1-126">**Para usar SQLLine**</span><span class="sxs-lookup"><span data-stu-id="101b1-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="101b1-127">Conéctese al clúster con SSH.</span><span class="sxs-lookup"><span data-stu-id="101b1-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="101b1-128">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="101b1-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="101b1-129">Desde SSH, introduzca los siguientes comandos para ejecutar SQLLine:</span><span class="sxs-lookup"><span data-stu-id="101b1-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="101b1-130">Ejecute los siguientes comandos para crear una tabla de HBase e insertar algunos datos:</span><span class="sxs-lookup"><span data-stu-id="101b1-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="101b1-131">Para más información, consulte el [manual de SQLLine](http://sqlline.sourceforge.net/#manual) y la [gramática de Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="101b1-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="101b1-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="101b1-132">Next steps</span></span>
<span data-ttu-id="101b1-133">En este artículo, ha aprendido cómo utilizar Phoenix Apache en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="101b1-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="101b1-134">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="101b1-134">To learn more, see:</span></span>

* <span data-ttu-id="101b1-135">[Información general de HBase de HDInsight][hdinsight-hbase-overview]: HBase es una base de datos NoSQL de código abierto Apache basada en Hadoop que proporciona acceso aleatorio y una coherencia sólida para grandes cantidades de datos no estructurados y semiestructurados.</span><span class="sxs-lookup"><span data-stu-id="101b1-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="101b1-136">[Aprovisionamiento de clústeres de HBase en Azure Virtual Network][hdinsight-hbase-provision-vnet]: con la integración de redes virtuales, los clústeres de HBase se pueden implementar en la misma red virtual que sus aplicaciones para que estas puedan comunicarse directamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="101b1-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="101b1-137">[Configuración de la replicación de HBase en HDInsight](hdinsight-hbase-replication.md): aprenda a configurar la replicación de HBase entre dos centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="101b1-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="101b1-138">[Análisis de sentimiento de Twitter con HBase en HDInsight][hbase-twitter-sentiment]: descubra cómo realizar [análisis de sentimiento](http://en.wikipedia.org/wiki/Sentiment_analysis) en tiempo real de macrodatos con HBase en un clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="101b1-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
